#最简单的向不支持NDK的工程添加C++ 方法（未引入第三方外库）


1. 创建C++代码文件夹cpp（APP/src/main/cpp 与正常的代码JAVA层平级）
2. 右键，在cpp目录下创建C/C++Source File,(new下面有选项，不用自己乱写，创建时勾选创建.h 文件)
3. .h文件定义方法，.cpp文件实现方法</br>
	.h文件可以省略，将所有引用移到.cpp 中即可，也不需要在.cpp中声明方法。</br>
 .h文件需要引入 jni.h头文件，（`#include <jni.h>`)以及声明 (`extern "C"`)</br>
 .cpp文件需要引入.h文件（`#include "XXX.h"`）</br>
 其他宏定义，会在生成文件时，自动生成
6. 在moudle的根目录下创建CMakeLists.txt文件（工程就是工程的根目录下）,并添加文件配置</br>

	    cmake_minimum_required(VERSION 3.4.1)
		add_library( 
			         trying`添加的lib名字`
			         SHARED 
			         src/main/cpp/trying.cpp )
		find_library( 
			          log-lib
			          log )
		target_link_libraries( 
			                   trying
			                   ${log-lib} )
			                   `具体说明见文件自带的注释`
7. 在当前项目中的build.gradle 中添加c++的编译配置及CMakeList.txt的引用

	在defaultConfig{}中添加
   
	     externalNativeBuild {
	     cmake {
	            cppFlags ""
	            }
	        }
        
	在Android{}最后面添加
	
	    externalNativeBuild {
	        cmake {
	            path "CMakeLists.txt"
	        }
	    }
    
8. 在JAVA代码中引用：
 	首先要载入库，再进行方法调用。直接调用在JAVA中定义的native方法即可，不用单独声明或引入其他。
 	
	 	 static {
	        System.loadLibrary("trying");
	    }   