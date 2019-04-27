# tvm_phone
tvm arm gpu opencl

2019.4.27

# TVM:�ֻ�[gpu|cpu]������Tensorflowģ��
## Ŀ��
�������ֻ�������tvm�Ĺ���,��gpu/cpu�������.
�ֻ�������tvm�Ļ������ǵ�Ҫ֧��android��ios����ƽ̨����c++����߿���ֲ��.

## �ֻ�cpu����TVM
��c++����tvm���ο�����ĩβ�� [�ο�2](#ref2) �� [�ο�3](#ref3) �Ϳ�����.

## �ֻ�gpu����TVM
### ����һ������ֻ��Ƿ�֧��gpu
���ֻ��ϰ�װ [�ο�5(Opencl-Z)](#ref5)���ܲ鿴�ֻ�gpu��Ϣ��
��Ϊmate7������֧��gpu����.
��Ϊ��â5������֧��gpu���㣬��tvm�����г���.
��ΪMate10/P10/С��6�Ϳ�������tvm, ��Ϊ��â5/С��5�Ͳ��С�

### ׼��TVM C++����
Ҫ���ֻ�������gpu����Ҫ�ο�����ĩβ��[�ο�4](#ref4)����.
[�ο�4](#ref4)��[�ο�2](#ref2)/[3](#ref3)�������ǣ�
`device_type��kDLCPU�����kDLGPU.`

Ϊ�����ֻ�������gpu��[�ο�4](#ref4)�ڵ� kDLGPU��Ҫ�޸ĳ� kDLOpenCL;

���ֱ�Ӳ�����gpu���ݣ�opencl�ᱨ�����:
`OpenCL Error, code=-38: CL_INVALID_MEM_OBJECT`

[�ο�4](#ref4)��[�ο�2](#ref2)/[3](#ref3)����һ����Ҫ�����𣬾��Ƕ�����/������ݵĴ���
Ϊ�˰����ݸ��ƽ�gpu,������� `TVMArrayCopyFromBytes`��
Ϊ�˰����ݴ�gpu���Ƴ������������ `TVMArrayCopyToBytes`��

### TVM device_type
Pc��ʹ��nvida gpu�Ļ�����̽ӿ���cuda.
�ֻ���ʹ��gpu�Ļ�����̽ӿ���Ҫ��OpenCL��.
1. ��tvm�ڣ�Ҫʹ��cpu�Ļ�������device_type��kDLCPU(1)��
2. Ҫʹ���ֻ�opencl gpu�Ļ�������device_type��kDLOpenCL(4)��
3. Ҫʹ��pc nvida gpu�Ļ�������device_type��kDLGPU(2)

### ׼��opencl.h��.so�ļ�
����tvm����Ҫopencl��ͷ�ļ�.
��[�ο�6](#ref6)����opencl.hͷ�ļ�.
�ֻ��ϱ���tvm������Ҫ libOpenCL.so�ļ�.
����ֱ�Ӵ�����ֻ��ڣ��ҵ�libOpenCL.so�������������ŵ����ndkĿ¼��ȥ.
�ҵ��ֻ���pc�ϵ�ndkĿ¼λ�ã�  

|�ֻ�ָ�|���ֻ�������|���Ƶ�NDKĿ¼|
|--|--|--|
|Armeabi-v7|/vendor/lib/libOpenCL.so|C:\Users\<your name>\AppData\Local\Android\Sdk\android-ndk-r19\ndk-bundle\toolchains\llvm\prebuilt\windows-x86_64\lib64\clang\8.0.2\lib\linux\arm|
|Arm64-v8|/vendor/lib64/libOpenCL.so|C:\Users\<your name>\AppData\Local\Android\Sdk\android-ndk-r19\ndk-bundle\toolchains\llvm\prebuilt\windows-x86_64\lib64\clang\8.0.2\lib\linux\aarch64|

### ׼���ֻ�UI
׼�������ϵ�c++����,opencl.h/.so,�Ϳ��Ա����tvm so���ļ��ˡ�
Ϊ�����ֻ���������������Ҫjava UI���档
������tvm�Դ���android demo([�ο�7](#ref7))�����������������
Tvm�Դ��Ĵ����������������ݣ��������ڵ�����linux���ֻ����linux�±��롣

### ����tvm
�����android demo app�󣬾������ֻ��ϲ����ˡ�


## �ֻ�gpu�����ٶȲ���
����ʹ��gpu��Ŀ����Ϊ������ٶȣ����Ǿ�˵��opencl��һ��bug������tvm gpu���ֻ���ʧȥ���ٶ����ơ�
. ����1�ǣ�tvm��һ�μ�������ģ�ͣ�opencl���û�ǳ�����Ȼ�����ͻ�����������ֻ�app���������������ǲ������ܵġ�

. ����2�ǣ�tvmʹ��gpu�Ļ�������(run)ȷʵ�ܿ죬����Ҫȡ������(run)�Ľ����get_output����ȴ�ǳ�����
����2�μ�[�ο�8](#ref8)��

���ǵ����������⣬���ֻ��ϣ�������cpu�ɣ�gpu��û��ʵ�á�

# �ο�

## ���ʽ���:
����1t TVM: �Ż�ģ�������ٶȣ����������ֻ������еĶ����ƴ��롣����2GPU����cpu����죬ר�����ڴ���������.����3Tensorflow: google�Ƶ��˹�����ģ��ѵ�����.

## �ο�����:
### �ο�1{#ref1}
tvm��վ https://tvm.ai/

### �ο�2{#ref2}
��CPP��ʹ��TVM������mxnetģ�ͣ���InsightfaceΪ����
https://zhuanlan.zhihu.com/p/55996985?utm_source=wechat_timeline&utm_medium=social&utm_oi=882552529345466368&from=timeline

### �ο�3{#ref3}
һ��һ����������������TVM(��)����TVM���C++�˵Ĳ���
https://zhuanlan.zhihu.com/p/60981432

### �ο�4�ֻ�������tvm gpu c++{#ref4}
tvm_deploy_gpu_sample.cpp
https://gist.github.com/masahi/d6ad36890d087f866de185f19aac3814

### �ο�5Opencl-Z app{#ref5}
��� android�Ƿ�֧�� opencl(GPU)
https://stackoverflow.com/questions/26795921/does-android-support-opencl
You can use OpenCL-Z Android to check the available and capabilities of OpenCL on Android devices.
OpenCL-Z apk:
https://www.allfreeapk.com/opencl-z,1359401/download.html

### �ο�6���� opencl.h{#ref6}
https://stackoverflow.com/questions/29082524/android-studio-fatal-error-cl-cl-h-no-such-file-or-directory

### �ο�7 Tvm��android demo(linux ){#ref7}
Apps/android_deploy
https://github.com/dmlc/tvm/tree/master/apps/android_deploy

### �ο�8 How to make the GPU to CPU memory copy faster? #979{#ref8}
https://github.com/dmlc/tvm/issues/979?from=timeline

clEnqueueReadBuffer is too slow
https://stackoverflow.com/questions/32190761/clenqueuereadbuffer-is-too-slow?from=timeline

