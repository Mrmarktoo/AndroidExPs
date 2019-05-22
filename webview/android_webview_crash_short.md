### webview长按闪退
------

```

System.err: android.content.res.Resources$NotFoundException: Resource ID #0x2090000
System.err:     at android.content.res.Resources.getValue(Resources.java:1566)
System.err:     at android.content.res.Resources.loadXmlResourceParser(Resources.java:3147)
System.err:     at android.content.res.Resources.getLayout(Resources.java:1322)
System.err:     at android.view.MenuInflater.inflate(MenuInflater.java:107)
System.err:     at androidx.appcompat.view.SupportMenuInflater.inflate(SupportMenuInflater.java:120)
System.err:     at org.chromium.content.browser.SelectActionModeCallback.createActionMenu(SelectActionModeCallback.java:123)
System.err:     at org.chromium.content.browser.SelectActionModeCallback.onCreateActionMode(SelectActionModeCallback.java:104)
System.err:     at com.android.internal.policy.impl.PhoneWindow$DecorView$ActionModeCallbackWrapper.onCreateActionMode(PhoneWindow.java:3511)
System.err:     at androidx.appcompat.view.SupportActionModeWrapper$CallbackWrapper.onCreateActionMode(SupportActionModeWrapper.java:159)
System.err:     at androidx.appcompat.app.AppCompatDelegateImpl$ActionModeCallbackWrapperV9.onCreateActionMode(AppCompatDelegateImpl.java:2357)
System.err:     at androidx.appcompat.app.AppCompatDelegateImpl.startSupportActionModeFromWindow(AppCompatDelegateImpl.java:1137)
System.err:     at androidx.appcompat.app.AppCompatDelegateImpl.startSupportActionMode(AppCompatDelegateImpl.java:1021)
System.err:     at androidx.appcompat.app.AppCompatDelegateImpl$AppCompatWindowCallback.startAsSupportActionMode(AppCompatDelegateImpl.java:2821)
System.err:     at androidx.appcompat.app.AppCompatDelegateImpl$AppCompatWindowCallback.onWindowStartingActionMode(AppCompatDelegateImpl.java:2803)
System.err:     at androidx.appcompat.view.WindowCallbackWrapper.onWindowStartingActionMode(WindowCallbackWrapper.java:155)
System.err:     at com.android.internal.policy.impl.PhoneWindow$DecorView.startActionMode(PhoneWindow.java:2896)
System.err:     at com.android.internal.policy.impl.PhoneWindow$DecorView.startActionModeForChild(PhoneWindow.java:2879)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.ViewGroup.startActionModeForChild(ViewGroup.java:732)
System.err:     at android.view.View.startActionMode(View.java:4975)
System.err:     at org.chromium.content.browser.ContentViewCore.showSelectActionBar(ContentViewCore.java:2149)
System.err:     at org.chromium.content.browser.ContentViewCore.onSelectionEvent(ContentViewCore.java:2206)
System.err:     at org.chromium.android_webview.AwContents.nativeOnDraw(Native Method)
System.err:     at org.chromium.android_webview.AwContents.access$4300(AwContents.java:90)
System.err:     at org.chromium.android_webview.AwContents$AwViewMethodsImpl.onDraw(AwContents.java:2663)
System.err:     at org.chromium.android_webview.AwContents.onDraw(AwContents.java:1132)
System.err:     at com.android.webview.chromium.WebViewChromium.onDraw(WebViewChromium.java:1601)
System.err:     at android.webkit.WebView.onDraw(WebView.java:2531)
System.err:     at android.view.View.draw(View.java:15526)
System.err:     at android.view.View.buildDrawingCacheImpl(View.java:14739)
System.err:     at android.view.View.buildDrawingCache(View.java:14594)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14389)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.View.draw(View.java:15235)
System.err:     at android.view.ViewGroup.drawChild(ViewGroup.java:3548)
System.err:     at android.view.ViewGroup.dispatchDraw(ViewGroup.java:3341)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14407)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ViewGroup.recreateChildDisplayList(ViewGroup.java:3532)
System.err:     at android.view.ViewGroup.dispatchGetDisplayList(ViewGroup.java:3511)
System.err:     at android.view.View.updateDisplayListIfDirty(View.java:14365)
System.err:     at android.view.View.getDisplayList(View.java:14444)
System.err:     at android.view.ThreadedRenderer.updateViewTreeDisplayList(ThreadedRenderer.java:279)
System.err:     at android.view.ThreadedRenderer.updateRootDisplayList(ThreadedRenderer.java:285)
System.err:     at android.view.ThreadedRenderer.draw(ThreadedRenderer.java:335)
System.err:     at android.view.ViewRootImpl.draw(ViewRootImpl.java:3051)
System.err:     at android.view.ViewRootImpl.performDraw(ViewRootImpl.java:2864)
System.err:     at android.view.ViewRootImpl.performTraversals(ViewRootImpl.java:2448)
System.err:     at android.view.ViewRootImpl.doTraversal(ViewRootImpl.java:1351)
System.err:     at android.view.ViewRootImpl$TraversalRunnable.run(ViewRootImpl.java:6820)
System.err:     at android.view.Choreographer$CallbackRecord.run(Choreographer.java:804)
System.err:     at android.view.Choreographer.doCallbacks(Choreographer.java:607)
System.err:     at android.view.Choreographer.doFrame(Choreographer.java:576)
System.err:     at android.view.Choreographer$FrameDisplayEventReceiver.run(Choreographer.java:790)
System.err:     at android.os.Handler.handleCallback(Handler.java:815)
System.err:     at android.os.Handler.dispatchMessage(Handler.java:104)
System.err:     at android.os.Looper.loop(Looper.java:224)
System.err:     at android.app.ActivityThread.main(ActivityThread.java:5958)
System.err:     at java.lang.reflect.Method.invoke(Native Method)
System.err:     at java.lang.reflect.Method.invoke(Method.java:372)
System.err:     at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:1113)
System.err:     at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:879)
chromium: [FATAL:jni_android.cc(295)] Check failed: false. Please include Java exception stack in crash report

D/PSD: set_ps_threshold: low_threshold 135 high_threshold 155 ps_average 75 algo_state 1

google-breakpad: ### ### ### ### ### ### ### ### ### ### ### ### ###
google-breakpad: Chrome build fingerprint:
google-breakpad: 1.0.0
google-breakpad: 1
google-breakpad: d0979a1e-0d81-4c4d-97cc-f4253b4e9c74
google-breakpad: ### ### ### ### ### ### ### ### ### ### ### ### ###
chromium: ### WebView Version 43.0.2357.121 (code 52357121)
libc: Fatal signal 6 (SIGABRT), code -6 in tid 16219 (app.package.name)

Build fingerprint: 'OPPO/A59m/A59:5.1/LMY47I/1515760704:user/release-keys'
AEE/AED: Revision: '0'
AEE/AED: ABI: 'arm64'
AEE/AED: pid: 16219, tid: 16219, name: app.package.name  >>> package.name <<<
AEE/AED: signal 6 (SIGABRT), code -6 (SI_TKILL), fault addr --------

AEE/AED: Abort message: '[FATAL:jni_android.cc(295)] Check failed: false. Please include Java exception stack in crash report

AEE/AED:     x0   0000000000000000  x1   0000000000003f5b  x2   0000000000000006  x3   0000007f995abe30
AEE/AED:     x4   0000007f995abe30  x5   0000000000000005  x6   0000000000000001  x7   0000000000000020
AEE/AED:     x8   0000000000000083  x9   000000000000000a  x10  0000000000000009  x11  0000000000000001
AEE/AED:     x12  0000000000000001  x13  20657361656c5020  x14  206564756c636e69  x15  0000007f993585a8
AEE/AED:     x16  0000007f9934a5f8  x17  0000007f992e905c  x18  0000000000000000  x19  0000007f995abe30
AEE/AED:     x20  0000007f995ac0e8  x21  0000007f99350000  x22  000000000000000b  x23  0000000000000006
AEE/AED:     x24  0000007fcdbc8c90  x25  0000007fcdbc8ca0  x26  0000007fcdbc8c50  x27  0000007f82dff430
AEE/AED:     x28  0000000000100021  x29  0000007fcdbc8640  x30  0000007f992a93c0
AEE/AED:     sp   0000007fcdbc8640  pc   0000007f992e9064  pstate 0000000060000000
AEE/AED: backtrace:
AEE/AED:     #00 pc 0000000000060064  /system/lib64/libc.so (tgkill+8)
AEE/AED:     #01 pc 00000000000203bc  /system/lib64/libc.so (pthread_kill+160)
AEE/AED:     #02 pc 00000000000218f0  /system/lib64/libc.so (raise+28)
AEE/AED:     #03 pc 000000000001b1fc  /system/lib64/libc.so (abort+60)
AEE/AED:     #04 pc 00000000006c2cc4  /system/app/WebViewGoogle/lib/arm64/libwebviewchromium.so

 ```
 