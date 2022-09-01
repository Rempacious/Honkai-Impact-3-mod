# Honkai Impact 3 mod

针对 崩坏3rd 的悬浮菜单mod

## 特点
1. 适用于国外区服
2. 动态抓取offset，故适用于当前及以后的任意游戏版本
3. 适配arm64-v8a、armeabi-v7a
4. 适用于安卓手机、安卓模拟器（主流模拟器会调用armeabi-v7a架构）
5. 不夹带私货（比如 广告）

## 食用方法
详情见 tutorial.docx

* 反编译游戏apk，生成对应文件夹
* 添加悬浮权限	
  * <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>
  * ![image](https://github.com/JMBQ/image/blob/main/Honkai-Impact-3-mod/01.png)
* 添加悬浮窗服务	
  * <service		android:name="com.android.support.Launcher"		android:enabled="true" 	android:exported="false" 	android:stopWithTask="true"/>
  * ![image](https://github.com/JMBQ/image/blob/main/Honkai-Impact-3-mod/02.png)
* 将com\android\support里的所有smali文件放入游戏文件夹中的android\support
  * ![image](https://github.com/JMBQ/image/blob/main/Honkai-Impact-3-mod/03.png)
* 打开com\miHoYo\overridenativeactivity\OverrideNativeActivity.smali，找到onCreate方法，在方法开头插入
  * invoke-static {p0}, Lcom/android/support/Main;->Start(Landroid/content/Context;)V
  * ![image](https://github.com/JMBQ/image/blob/main/Honkai-Impact-3-mod/04.png)
* 将libSaber、libArcher这2个文件放入游戏目录assets文件夹内
  * ![image](https://github.com/JMBQ/image/blob/main/Honkai-Impact-3-mod/05.png)
* 编译游戏文件夹，生成直装包


## 注意事项
* 首次运行游戏，在正常情况下会跳至悬浮权限界面
* 刚打开游戏就闪退：saber\archer动态库已加密，运行时解密而导致的
  * 偶尔出现刚打开就闪退 属于正常现象
  * 连续多次出现刚打开就闪退 属于不正常现象，检查制作是否操作错误
* 游戏中途正常情况下不会闪退、卡住
* 如果出现游戏卡住，但悬浮菜单可以正常移动及操作，这种情况是触发了mod自身运行环境检测，mod主动击溃游戏进程
