# JNI

LD_LIBRARY_PATH  
CLASS_PATH  
生成相应的 C/C++ 头文件
javah -jni clsaa_name   

```
# 使用时在文件目录，如
JniForDriver/
└── Led.class
则使用如下命令 在当前文件夹生成 JniForDriver_Led.h文件
javah -jni JniForDriver.Led
```


```java
//JAVA中申明
public native void hello();//使用时申明
```
1. 加载C库  

```java
System.loadLibrary("native");/*加载 libnative.so*/

```
2. 映射 (在C语言中实现)  

```c
#include <jni.h>

JNIEXPORT jint JNICAL

JNI_OnLoad(JavaVM *jvm, void *reserved)
{
  JNIEnv *env;
  jclass cls;
  cached_jvm = jvm; /* cache the JavaVM pointer */
  if ((*jvm)->GetEnv(jvm, (void **)&env, JNI_VERSION_1_2))
  {
    return JNI_ERR; /* JNI version not supported */
  }
  cls = (*env)->FindClass(env, "C");
  if (cls == NULL)
  {
    return JNI_ERR;
  }
  /* Use weak global ref to allow C class to be unloaded */
  Class_C = (*env)->NewWeakGlobalRef(env, cls);
  if (Class_C == NULL)
  {
    return JNI_ERR;
  }
  /* Compute and cache the method ID */
  MID_C_g = (*env)->GetMethodID(env, cls, "g", "()V");
  if (MID_C_g == NULL)
  {
    return JNI_ERR;
  }
  return JNI_VERSION_1_2;
}  
```
3. 调用  
