# tvm-android-demo
tvm android arm gpu opencl

2019.4.29

## Ŀ��

   TVM �Դ��� android demo, ����ʱ����������:

   ����1. ��Ҫ�õ� android ndk, opencl ͷ�ļ���opencl���ļ���
   ����2. ��Ϊ��build.sh����ndk-build,���������linux�±���
   ����3. ���뻹��Ҫ tvm jar:[tvm4j-core-0.0.1-SNAPSHOT.jar]()
   
   �⵼�±�����̱Ƚ�ʹ�죬������һЩʱ�䣬���ѱ����app.

   ���ԣ��Ұ��Լ������apk�ų����������ֻ����android��������һ�� tvm ���ٶȣ��������ر�app��

   �Ұ�������opencl/tvm jar,���ŵ���Դ�����ڣ�������ֻҪ��android studio�Ϳ��Ա������app.
 
 
## ����
   ������վ�û��������pub
   [tvm android demo apk](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy/app/build/outputs/apk/debug/app-debug.apk)
   android demo Դ���� [tvm android demo](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy)
   [tvm4j-core-0.0.1-SNAPSHOT.jar](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy/app/src/main/libs)
   [libOpenCL.so](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy/app/src/main/jni/opencl/jnilibs)
   [libtvm4j_runtime_packed.so](https://zwd.3wfocus.com/!/#files/view/head/trunk/tp/tvm/apps/android_deploy/app/src/main/jnilibs)
   


## ���빦��
1. ��ѡ��CPU����GPU��Ȼ���ټ��� tvm ���п�
2. ѡ��ͼƬ����tvm��������Ȼ����ʾ�����ѵ�ʱ��

## �Ķ���
1. �Դ���90Mģ���ļ��������ʱ����������
2. ������ build.sh ���� libtvm4j_runtime_packed.so ����� CMakeLists.txt
3. ������ opencl ͷ�ļ��� so. libOpenCL.so �Ǵӻ�ΪP10�ֻ��ڸ��Ƴ�����
4. �Դ��� tvm4j-core-0.0.1-SNAPSHOT.jar, ������������
5. �Դ��� libtvm4j_runtime_packed.so, Ҳ���ñ���so��
6. ��tvmģ�͵����� so �� arm64, ������ֻ������ arm64.
   `build.gradle: abiFilters 'arm64-v8a'`
   tvmģ�͵�����so: 
   `apps\android_deploy\app\src\main\assets\deploy_lib_cpu.so/deploy_lib_opencl.so`
