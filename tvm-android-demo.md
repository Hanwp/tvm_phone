# tvm-android-demo

[tvm android arm gpu opencl](https://github.com/zhaowd2001/tvm_phone/blob/master/tvm-android-demo.md)

2019.4.29 第一版
2019.5.16 增加armv7 c++源代码: TVMModelApi.java, tvm_model_api.cc

## 下载
   - 下载需要的用户名口令都是pub
   - tvm android demo apk 
   [arm64 apk](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/build/outputs/apk/debug/app-debug.apk)
   [armv7 apk](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy_2_armv7/app/build/outputs/apk/debug/app-debug.apk)

- tvm android demo 源代码: android studio
   [android_deploy arm64 工程](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy)
   [android_deploy_2_armv7 armv7 工程](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy_2_armv7)
   - [android_deploy_3_armv7_cpp armv7 c++ 工程](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy_3_armv7_cpp)
   - [android_deploy_3_armv7_cpp armv7 c++ 源代码](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy_3_armv7_cpp/app/src/main/jni/tvm_model_api.cc)
   - [android_deploy_3_armv7_cpp armv7 c++ 测试代码](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy_3_armv7_cpp/app/src/main/java/cn/TVMModelApi.java)

- [tvm jar : tvm4j-core-0.0.1-SNAPSHOT.jar](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/libs/tvm4j-core-0.0.1-SNAPSHOT.jar)

- [手机gpu的运行库: libOpenCL.so](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/jni/opencl/jnilibs)

- [tvm 运行库: libtvm4j_runtime_packed.so](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/jnilibs)
   

## 目的
   提供能直接安装到android手机上，运行起来的 tvm demo 安装包.

   同时提供android studio源代码，只需要android studio就能编译出 tvm demo 安装包.
   
   TVM 自带的 android demo, 编译时有以下小问题:

   - 问题1. 需要用到 android ndk, opencl 头文件和opencl库文件.
   
   - 问题2. 因为用build.sh调用ndk-build, 只能在 linux 下编译.
   
   - 问题3. 编译还需要 tvm jar:[tvm4j-core-0.0.1-SNAPSHOT.jar](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/libs/tvm4j-core-0.0.1-SNAPSHOT.jar)
   
   这导致编译过程比较曲折，不花费一些时间，很难编译出app.

   所以，我把自己编译的apk放出来，如果你只想在android上体验上一下 tvm 的速度，可以下载本app。

   同时,我把依赖的opencl/tvm jar,都放到了源代码内，这样你只要用android studio就可以编译出本app.
 

## 代码功能
   1. 能选择CPU还是GPU，然后再加载 tvm 运行库
   2. 选择图片后，用tvm进行推理，然后显示推理花费的时间

## 代码改动点
1. 自带了90M模型文件，编译的时候不用联网下载了
   tvm模型的两个 so 是 arm64, 所以我只编译了 arm64.
   `build.gradle: abiFilters 'arm64-v8a'`
   tvm模型的两个so: 
   `apps\android_deploy\app\src\main\assets\deploy_lib_cpu.so/deploy_lib_opencl.so`
2. 命令行 build.sh 编译 libtvm4j_runtime_packed.so，改成了用 CMakeLists.txt 编译 so
3. 添加了 opencl 头文件和 so.
   libOpenCL.so 是从华为P10手机内复制出来的
4. 添加了 tvm4j-core-0.0.1-SNAPSHOT.jar, 不用再去编译了
5. 添加了 libtvm4j_runtime_packed.so, 也不用编译tvm运行库了

## 编译tvm运行库
   tvm的android运行库是libtvm4j_runtime_packed.so
   我提供的代码内，是连接到libOpenCL.so的gpu版本.
   下面描述如何编译gpu和cpu两个版本的运行库.
   1. 编译 cpu 版本运行库
   - 删除源代码内的所有 libtvm4j_runtime_packed.so. 
     so在这个目录 `apps\android_deploy\app\src\main\jnilibs`
   - 把 `apps\android_deploy\app\build-cpu.gradle` 覆盖到
     `apps\android_deploy\app\build.gradle` . 
   - 把 `apps\android_deploy\app\CMakeLists-cpu.txt` 覆盖到
     `apps\android_deploy\app\CMakeLists.txt` . 
   - 重新编译 android_deploy，生成的tvm运行库就是 cpu 版本的运行库.
   新生成的库在下面的目录: `apps\android_deploy\app\build\intermediates\transforms\stripDebugSymbol\release\0\lib\`

   2. 编译 tvm gpu 版本运行库
   - 删除源代码内的所有 libtvm4j_runtime_packed.so. 
     so在这个目录 `apps\android_deploy\app\src\main\jnilibs`
   - 把 `apps\android_deploy\app\build-gpu.gradle` 覆盖到
     `apps\android_deploy\app\build.gradle` . 
   - 把 `apps\android_deploy\app\CMakeLists-gpu.txt` 覆盖到
     `apps\android_deploy\app\CMakeLists.txt` . 
   - 把 libOpenCL.so 复制到ndk的lib目录.
     手机上编译tvm，还需要 libOpenCL.so文件.
     可以直接从你的手机内，找到libOpenCL.so，下载下来，放到你的ndk目录内去.
     我的手机和pc上的ndk目录位置：  

|手机指令集|从手机上下载|复制到NDK目录|
|--|--|--|
|Armeabi-v7|/vendor/lib/libOpenCL.so|C:\Users\<your name>\AppData\Local\Android\Sdk\android-ndk-r19\ndk-bundle\toolchains\llvm\prebuilt\windows-x86_64\lib64\clang\8.0.2\lib\linux\arm|
|Arm64-v8|/vendor/lib64/libOpenCL.so|C:\Users\<your name>\AppData\Local\Android\Sdk\android-ndk-r19\ndk-bundle\toolchains\llvm\prebuilt\windows-x86_64\lib64\clang\8.0.2\lib\linux\aarch64|

   - 重新编译 android_deploy，生成的tvm运行库就是 gpu 版本的运行库.
   新生成的库在下面的目录: `apps\android_deploy\app\build\intermediates\transforms\stripDebugSymbol\release\0\lib\`
