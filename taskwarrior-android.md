
## Tiny troubleshooting guide for [TaskwarriorAndroid](https://bitbucket.org/kvorobyev/taskwarriorandroid):

  * make sure you transfer your files in unix mode
  
  If you try to click on Settings and Taskwarrior is unable to open the file even though you just placed it in the correct directory 
  then your files may have some unwanted carriage returns (CR/LF). Make sure to save and transfer them in unix mode -- 
  that is, line feeds only.
  
  * If you get an `open failed: EACCES (Permission denied)` error message you propably didn't allow TaskWarrior to access your Storage.
    The full error message looks somthing like this:    
  ```
14:02:06: Device is: bq Aquaris X5 Plus armeabi-v7a 23
14:02:06: Application is: 0.1.1604102123 1604102123
14:02:06: Profile: jayne 1b76ab05-db81-458e-9135-355a2590a0cd /storage/emulated/0/Android/data/kvj.taskw/files/1b76ab05-db81-458e-9135-355a2590a0cd, exist: true, isFile: false, isFolder: true, canRead: true, canWrite: true, size: 4096
14:02:06: taskd.* config: {taskd.ca=intermediate.pem, taskd.certificate=cert.pem, taskd.key=key.pem, taskd.server=taskdserver:53589, taskd.trust=strict}
14:02:06: Host and port: taskdserver 53589
14:02:06: CA file: /storage/emulated/0/Android/data/kvj.taskw/files/1b76ab05-db81-458e-9135-355a2590a0cd/intermediate.pem, exist: true, isFile: true, isFolder: false, canRead: false, canWrite: false, size: 1647
14:02:06: Certificate file: /storage/emulated/0/Android/data/kvj.taskw/files/1b76ab05-db81-458e-9135-355a2590a0cd/cert.pem, exist: true, isFile: true, isFolder: false, canRead: true, canWrite: true, size: 1948
14:02:06: Key file: /storage/emulated/0/Android/data/kvj.taskw/files/1b76ab05-db81-458e-9135-355a2590a0cd/key.pem, exist: true, isFile: true, isFolder: false, canRead: false, canWrite: false, size: 10996
java.io.FileNotFoundException: /storage/emulated/0/Android/data/kvj.taskw/files/1b76ab05-db81-458e-9135-355a2590a0cd/intermediate.pem: open failed: EACCES (Permission denied)
	at libcore.io.IoBridge.open(IoBridge.java:452)
	at de.robv.android.xposed.XposedBridge.invokeOriginalMethodNative(Native Method)
	at de.robv.android.xposed.XposedBridge.handleHookedMethod(XposedBridge.java:334)
	at libcore.io.IoBridge.open(<Xposed>)
	at java.io.FileInputStream.<init>(FileInputStream.java:76)
	at kvj.taskw.data.AccountController$LocalSocketRunner.<init>(AccountController.java:740)
	at kvj.taskw.data.AccountController$LocalSocketRunner.<init>(AccountController.java:718)
	at kvj.taskw.data.AccountController.openLocalSocket(AccountController.java:850)
	at kvj.taskw.data.AccountController.<init>(AccountController.java:199)
	at kvj.taskw.data.Controller.accountController(Controller.java:330)
	at kvj.taskw.ui.MainActivity$10.doInBackground(MainActivity.java:333)
	at kvj.taskw.ui.MainActivity$10.doInBackground(MainActivity.java:329)
	at org.kvj.bravo7.util.Tasks$SimpleTask.doInBackground(Tasks.java:15)
	at org.kvj.bravo7.util.Tasks$SimpleTask.doInBackground(Tasks.java:11)
	at android.os.AsyncTask$2.call(AsyncTask.java:295)
	at java.util.concurrent.FutureTask.run(FutureTask.java:237)
	at android.os.AsyncTask$SerialExecutor$1.run(AsyncTask.java:234)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1113)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:588)
	at java.lang.Thread.run(Thread.java:818)
Caused by: android.system.ErrnoException: open failed: EACCES (Permission denied)
	at libcore.io.Posix.open(Native Method)
	at libcore.io.BlockGuardOs.open(BlockGuardOs.java:186)
	at libcore.io.IoBridge.open(IoBridge.java:438)
	... 19 more
  
  ```
  If you see this sort of error you can enable the Storage permssions on Android 6 here:
   * open settings
      * select `Apps`
        * click the <confiugre button> in the top right corner
          * select`App permissions`
            * select `Storage`
              * enable it for TaskWarrior
              
  Don't forget to close TaskWarrior after this
   * again, open Settings
      * select `Apps`
        * scroll down to TaskWarrior
          * click on `FORCE STOP`
