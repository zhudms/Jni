#OpenCV Demo 的使用
1. File-->new-->importMoudle-->(openCV4Android -->sdk-->java)，将java代码导入工程

2. 将openCV4Android -->sdk/native/libs 修改名称为jniLibs，放入到目标工程app/src/main 目录下(只留下libopencv_java3.so文件即可)
3. 为了避免使用OpenCvManager.apk 在项目开始使用静态方式载入java3.so
 
 ```
   static {
        System.loadLibrary("opencv_java3");
    }
    ```
4. 修改onResume() 方法中的动态加载库方式（一般是删除就可以了），修改加载回调方式
5. 其他各项目不同。
6. build时moudle中JAVA代码报错，静态变量找不到，须修改sdk版本，目前自己用的tagertSDk是21
7. 人脸检测的demo见git工程openCV-offical-demo
8. color-blob-detection 彩色斑点检测
9. 