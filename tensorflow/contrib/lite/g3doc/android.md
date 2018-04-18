# TensorFlow Lite for Android

## Building

Basically, the environment to be prepared is the same as TensorFlow. See the README.md in tensorflow/contrib/makefile/

You can compile a TensorFlow Lite library for Android target. It can then be compiled into static or shared library as required.

First, you will need to download and unzip the [Native Development Kit (NDK)](https://developer.android.com/ndk/).
You will not need to install the standalone toolchain, however.

Assign your NDK location to $NDK_ROOT:

```bash
export NDK_ROOT=/absolute/path/to/NDK/android-ndk-rxxx/
```

To compile TensorFlow Lite library using the Makefile, you need the cpufeatures library in NDK.

```bash
mkdir -p $NDK_ROOT/sources/android/cpufeatures/jni
cp $NDK_ROOT/sources/android/cpufeatures/cpu-features.* $NDK_ROOT/sources/android/cpufeatures/jni
cp $NDK_ROOT/sources/android/cpufeatures/Android.mk $NDK_ROOT/sources/android/cpufeatures/jni
ndk-build NDK_PROJECT_PATH="$NDK_ROOT/sources/android/cpufeatures" NDK_APPLICATION_MK="$NDK_ROOT/sources/android/cpufeatures/Android.mk"
```

### Static library

Then, you will have complied a static library in 'gen/lib/android_${ANDROID_ARCH}/' compiled for Android as execute the following:

```bash
tensorflow/contrib/makefile/download_dependencies.sh
make -f tensorflow/contrib/makefile/Makefile TARGET=ANDROID
```

The resulting library name is libtensorflow-lite.a

### Shared library

If you compile as a shared library, execute the following command.
The resulting library name is libtensorflow-lite.so

```bash
make -f tensorflow/contrib/lite/Makefile TARGET=ANDROID SUB_MAKEFILES=tensorflow/contrib/lite/sub_makefiles/android/Makefile.in libtensorflow-lite.so
```
