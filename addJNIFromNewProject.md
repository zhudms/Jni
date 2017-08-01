#JNIInclude
 1. 创建库Moudle
 2. 在库 moudle 根目录中创建CMakeLists.txt文件
 3. 添加库目录（自己定义）
 4. 添加库代码文件
 4. 在库根目录下，创建CMakeLists.txt文件
 5. 写入配置
 
        cmake\_minimum_required(VERSION 3.4.1)

		add_library(trying SHARED
            src/main/cpp/trying.cpp)

        set(distribution\_DIR ${CMAKE_CURRENT_SOURCE_DIR}/../distribution)

		set\_target\_properties(trying PROPERTIES
		                      LIBRARY\_OUTPUT\_DIRECTORY
		                      ${distribution\_DIR}/libs/${ANDROID_ABI})
		                      
		target_include_directories(trying
		                           PUBLIC ${CMAKE\_CURRENT\_SOURCE_DIR}/src/main/cpp)
		                           
 6. 在模块的build.gradle中添加CMakeLists的引用，及编译条件
+ 在模块mathlib的build.gradle中的defaultConfig{}中添加如下语句：

        externalNativeBuild {
        cmake {
        arguments '-DANDROID_PLATFORM=android-19',
                  '-DANDROID_TOOLCHAIN=clang', '-DANDROID_STL=gnustl_static'
        targets 'add'
        }
        }
+ android{}最后添加如下语句，将CMakeLists.txt关联起来。

        externalNativeBuild {
   			 cmake {
        path 'CMakeLists.txt'
   			 }
		}
10. 在需要定义jni方法的地方，声明native方法，使用option+enter不全，会自动在main目录下，生成jni文件夹，并生成全小写文件名的.c文件（此时，JAVA中的声明代码仍然报红，不用理）





+这是未完成的攻略，问题太多，暂时搁置