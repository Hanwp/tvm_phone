# tvm-android-demo

[tvm android arm gpu opencl](https://github.com/zhaowd2001/tvm_phone/blob/master/tvm-android-demo.md)

2019.4.29
## ����
   - ������Ҫ���û��������pub
   - [tvm android demo apk](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/build/outputs/apk/debug/app-debug.apk)
   - [tvm android demo Դ����: android studio ](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy)
   - [tvm jar : tvm4j-core-0.0.1-SNAPSHOT.jar](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/libs/tvm4j-core-0.0.1-SNAPSHOT.jar)
   - [�ֻ�gpu�����п�: libOpenCL.so](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/jni/opencl/jnilibs)
   - [tvm ���п�: libtvm4j_runtime_packed.so](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/jnilibs)
   

## Ŀ��
   �ṩ��ֱ�Ӱ�װ��android�ֻ��ϣ����������� tvm demo ��װ��.
   ͬʱ�ṩandroid studioԴ���룬ֻ��Ҫandroid studio���ܱ���� tvm demo ��װ��.
   
   TVM �Դ��� android demo, ����ʱ������С����:

   - ����1. ��Ҫ�õ� android ndk, opencl ͷ�ļ���opencl���ļ�.
   
   - ����2. ��Ϊ��build.sh����ndk-build, ֻ���� linux �±���.
   
   - ����3. ���뻹��Ҫ tvm jar:[tvm4j-core-0.0.1-SNAPSHOT.jar](https://zwd.3wfocus.com/svn/files/trunk/tp/tvm/apps/android_deploy/app/src/main/libs/tvm4j-core-0.0.1-SNAPSHOT.jar)
   
   �⵼�±�����̱Ƚ����ۣ�������һЩʱ�䣬���ѱ����app.

   ���ԣ��Ұ��Լ������apk�ų����������ֻ����android��������һ�� tvm ���ٶȣ��������ر�app��

   ͬʱ,�Ұ�������opencl/tvm jar,���ŵ���Դ�����ڣ�������ֻҪ��android studio�Ϳ��Ա������app.
 

## ���빦��
   1. ��ѡ��CPU����GPU��Ȼ���ټ��� tvm ���п�
   2. ѡ��ͼƬ����tvm��������Ȼ����ʾ�����ѵ�ʱ��

## ����Ķ���
1. �Դ���90Mģ���ļ��������ʱ��������������
   tvmģ�͵����� so �� arm64, ������ֻ������ arm64.
   `build.gradle: abiFilters 'arm64-v8a'`
   tvmģ�͵�����so: 
   `apps\android_deploy\app\src\main\assets\deploy_lib_cpu.so/deploy_lib_opencl.so`
2. ������ build.sh ���� libtvm4j_runtime_packed.so���ĳ����� CMakeLists.txt ���� so
3. ����� opencl ͷ�ļ��� so.
   libOpenCL.so �Ǵӻ�ΪP10�ֻ��ڸ��Ƴ�����
4. ����� tvm4j-core-0.0.1-SNAPSHOT.jar, ������ȥ������
5. ����� libtvm4j_runtime_packed.so, Ҳ���ñ���tvm���п���
