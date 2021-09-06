### 第三方库使用注意事项汇总
------

### 1.[腾讯云 对象存储 回调结果在工作线程](/thirdlib/tencent_cos_thread_problem.md) 

``` kotlin

object TOSUtil {

    //    CosXmlServiceConfig 是 COS 服务的配置类
    private val projectId = "1257239906"
    private val region = "ap-beijing"
    private val bucket = "ddbes-repository-1257239906"

    private val serviceConfig: CosXmlServiceConfig = CosXmlServiceConfig.Builder().setRegion(region).isHttps(false).setDebuggable(true).builder()

    private var cosXmlService: CosXmlSimpleService? = null
    private var transferManager: TransferManager? = null

    class MyProvider(private val secretID: String, private val secretKey: String, val token: String, private val expiredTimeNumber: Long) : BasicLifecycleCredentialProvider() {

        override fun fetchNewCredentials(): QCloudLifecycleCredentials {
            // 首先从您的临时密钥服务器获取包含了签名信息的响应
            // 然后解析响应，获取密钥信息
//            val tmpSecretId = "COS_SECRETID" //临时密钥 secretId
//            val tmpSecretKey = "COS_SECRETKEY" //临时密钥 secretKey
//            val sessionToken = "TOKEN" //临时密钥 Token
//            val expiredTime = 1556183496L//临时密钥有效截止时间

//            // 返回服务器时间作为签名的起始时间
//            val beginTime = 1556182000L//临时密钥有效起始时间

            // todo something you want

            // 最后返回临时密钥信息对象
            return SessionQCloudCredentials(secretID, secretKey, token, 0L, expiredTimeNumber)
        }
    }

    fun getCustomSessinoCredential(secretID: String, secretKey: String, token: String, expiredTimeNumber: Long): BasicLifecycleCredentialProvider {
        return MyProvider(secretID, secretKey, token, expiredTimeNumber)
    }

    //    初始化授权类
    /*临时秘钥*/
    fun getSessionCredential(url: String, method: String = "GET"): QCloudCredentialProvider? {
        try {
            val uri = URL(url)
            return SessionCredentialProvider(HttpRequest.Builder<String>().url(uri).method(method).build())
        } catch (e: Exception) {
        }
        return null
    }

    /*获取固定秘钥*/
    fun getSolidCredential(): QCloudCredentialProvider {
        val secretId = ""
        val secretKey = ""
        return ShortTimeCredentialProvider(secretId, secretKey, 300)
    }

    private var expiredTimeNumber: Long = 0L

    fun initService(secretID: String, secretKey: String, token: String, expiredTimeNumber: Long) {
        this.expiredTimeNumber = expiredTimeNumber
        initService(BaseApplication.joinuTechContext, serviceConfig, getCustomSessinoCredential(secretID, secretKey, token, expiredTimeNumber))
//        initService(context, serviceConfig, getSessionCredential("you url"))
//        initService(context, serviceConfig, getSolidCredential())
    }

    fun isInited(): Boolean {
        return cosXmlService != null && transferManager != null
    }

    fun isOutDate(): Boolean {
        return expiredTimeNumber <= (System.currentTimeMillis() - 500)
    }

    //    初始化 CosXmlService 服务类
    private fun initService(context: Context, serviceConfig: CosXmlServiceConfig, credentialProvider: QCloudCredentialProvider?) {
        if (credentialProvider != null) {
            cosXmlService = CosXmlSimpleService(context, serviceConfig, credentialProvider)
            val transferConfig = TransferConfig.Builder()
//        若有特殊要求，则可以如下进行初始化定制。如限定当对象 >= 2M 时，启用分片上传，且分片上传的分片大小为 1M, 当源对象大于 5M 时启用分片复制，且分片复制的大小为 5M。
                    .setDividsionForCopy(5 * 1024 * 1024) // 是否启用分片复制的最小对象大小
                    .setSliceSizeForCopy(5 * 1024 * 1024) //分片复制时的分片大小
                    .setDivisionForUpload(2 * 1024 * 1024) // 是否启用分片上传的最小对象大小
                    .setSliceSizeForUpload(1024 * 1024) //分片上传时的分片大小
                    .build()

            transferManager = TransferManager(cosXmlService, transferConfig)

        }
    }

    //    桶相关  存储位置相关
    fun createBucket(bucketName: String, cosPath: String, srcPath: String) {
        cosXmlService?.putObjectAsync(PutObjectRequest(bucketName, cosPath, srcPath), object : CosXmlResultListener {
            override fun onSuccess(request: CosXmlRequest?, result: CosXmlResult?) {
                val putObjectRequest = result
            }

            override fun onFail(request: CosXmlRequest?, exception: CosXmlClientException?, serviceException: CosXmlServiceException?) {

            }
        })
    }

    fun getBucketList() {
        cosXmlService?.getObjectAsync(GetObjectRequest(), object : CosXmlResultListener {
            override fun onSuccess(request: CosXmlRequest?, result: CosXmlResult?) {

            }

            override fun onFail(request: CosXmlRequest?, exception: CosXmlClientException?, serviceException: CosXmlServiceException?) {

            }

        })
    }
    //    桶相关  存储位置相关

    fun uploadFile(filePath: String, userId: Long,
                   onProgress: ((complete: Long, target: Long) -> Unit?)? = null,
                   onSuccess: (request: String?, result: String?) -> Unit,
                   onFailed: (errcode: Int?, errMsg: String?, serviceErr: String?) -> Unit,
                   onState: (state: String) -> Unit) {

//        val cosPath = "对象键"//即对象到 COS 上的绝对路径, 格式如 cosPath = "text.txt";
//        val srcPath = "本地文件的绝对路径"// 如 srcPath=Environment.getExternalStorageDirectory().getPath() + "/text.txt";
        val file = File(filePath)
        if (!file.exists()) {
            return
        }
        val cosPath = projectId + "_" + userId + "_" + file.name//即对象到 COS 上的绝对路径, 格式如 cosPath = "text.txt";
        val srcPath = filePath// 如 srcPath=Environment.getExternalStorageDirectory().getPath() + "/text.txt";
        val uploadId = null //若存在初始化分片上传的 UploadId，则赋值对应 uploadId 值用于续传，否则，赋值 null。

        val cosxmlUploadTask: COSXMLUploadTask? = transferManager?.upload(bucket, cosPath, srcPath, uploadId)
        /**
         * 若是上传字节数组，则可调用 TransferManager 的 upload(string, string, byte[]) 方法实现;
         * byte[] bytes = "this is a test".getBytes(Charset.forName("UTF-8"));
         * cosxmlUploadTask = transferManager.upload(bucket, cosPath, bytes);
         */

        /**
         * 若是上传字节流，则可调用 TransferManager 的 upload(String, String, InputStream) 方法实现；
         * InputStream inputStream = new ByteArrayInputStream("this is a test".getBytes(Charset.forName("UTF-8")));
         * cosxmlUploadTask = transferManager.upload(bucket, cosPath, inputStream);
         */

        addListener(cosxmlUploadTask, onProgress, onSuccess, onFailed, onState)

//        return cosxmlUploadTask
    }

    private fun addListener(task: COSXMLUploadTask?,
                            onProgress: ((complete: Long, target: Long) -> Unit?)? = null,
                            onSuccess: (request: String?, result: String?) -> Unit,
                            onFailed: (errcode: Int?, errMsg: String?, serviceErr: String?) -> Unit,
                            onState: (state: String) -> Unit) {
        task?.apply {
            setCosXmlProgressListener { complete, target ->
                LogUtil.showLog("UpLoad progress $complete - $target")
                onProgress?.invoke(complete, target)
            }

            setCosXmlResultListener(object : CosXmlResultListener {
                override fun onSuccess(request: CosXmlRequest?, result: CosXmlResult?) {
                    LogUtil.showLog("UpLoad success ${request?.toString()} - ${result?.toString()}")
                    onSuccess.invoke(request?.toString(), result?.accessUrl)
                }

                override fun onFail(request: CosXmlRequest?, exception: CosXmlClientException?, serviceException: CosXmlServiceException?) {
                    LogUtil.showLog("UpLoad failed ${exception?.errorCode} - ${exception?.message} - ${serviceException?.toString()}")
                    onFailed.invoke(exception?.errorCode, exception?.message, serviceException?.message)
                }
            })

            setTransferStateListener {
                LogUtil.showLog("state is ${it.name}")
                onState.invoke(it.name)
            }
        }
    }

    fun uploadCancel(task: COSXMLUploadTask) {
        task.cancel()
    }

    fun uploadPause(task: COSXMLUploadTask) {
        task.pause()
    }

    fun uploadResume(task: COSXMLUploadTask) {
        task.resume()
    }

    fun downFile(url: String, savedDirPath: String, cosPath: String) {
        val downloadTask: COSXMLDownloadTask? = transferManager?.download(BaseApplication.joinuTechContext, bucket, cosPath, savedDirPath)
    }

}

data class TosUploadAuthBean(
        val credentials: Credentials,
        val expiredTime: Long
)

data class Credentials(
        val sessionToken: String,
        val tmpSecretId: String,
        val tmpSecretKey: String
)

```
 