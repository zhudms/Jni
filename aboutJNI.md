#老版本JNI
## 1. Application.mk
+ APP_STL=gnustl\_static
+ APP_CPPFLAGS:=-frtti -fexceptions 
+ APP_ABI:= armeabi-v7a (指定生成包，这个应该不是固定的)
+  在Application.mk里还可以配置APP_PLATFORM=17类似这种，当然不配置完全可以。

## 2. Android.mk


+ LOCAL\_PATH :=$(call my\-dir)
include $(CLEAR_VARS)


+ OpenCV\_INSTALL\_MODULES:=on(自动将依赖的OpenCV的so库拷贝到libs目录下，但很遗憾的是，这个命令只对OPENCV\_CAMERA_MODULES有效。(OpenCV)只有当OPENCV\_CAMERA_MODULES:=on时，可以看到他会自动将里面的带camera的so拷贝至工程下的libs文件夹下)

+ OPENCV\_CAMERA_MODULES:=off


+ OPENCV\_LIB_TYPE:=STATIC（静态注册，SHARE动态链接，动态链接需要将依赖的包，在代码中手动加载（生成的应用，在opencv的demo中比静态注册要大））


+ ifeq ("$(wildcard $(OPENCV_MK_PATH))","")
include D:\ProgramFile\OpenCV-2.4.9-android-sdk\sdk\native\jni\OpenCV.mk
else  
 include $(OPENCV_MK_PATH)  
endif 
（这句话比较关键，这是我安装OpenCV-2.4.9-android-sdk的地方，我将其安装到了D盘。而我的工作空间在E盘也是ok的）

+ LOCAL\_MODULE:=ProcessImg （是要生成的库的名字）

+ LOCAL\_SRC\_FILES := DetectFace\_JNI.cpp </br>
					src/copyToAssets.cpp</br> 
					src/detectFace.cpp</br>
					（jni文件夹下的cpp文件，其中的src说明我的jni下还有个子文件夹名字是“src”，这块替换成自己的源码文件就ok了）
+ LOCAL_LDLIBS    += -lm -llog 
			
+ include $(BUILD\_SHARED_LIBRARY) 
