# xHook Prefab

Prefab package for <https://github.com/iqiyi/xHook>.

## Changes to original

- Removed `__attribute__((visibility("default")))`
- Removed JNI interface (xh_jni.c)

## Integration

This is a [Prefab](https://google.github.io/prefab/) library, so you will need to enable it in your project (requires Android Gradle Plugin 4.1+):

```gradle
android {
    ...
    buildFeatures {
        ...
        prefab true
    }
}
```

Add dependency:

```gradle
repositories {
    mavenCentral()
}

dependencies {
    implementation 'dev.rikka.ndk.thirdparty:xhook:1.2.0'
}
```

## Usage

### ndk-build

```makefile
LOCAL_STATIC_LIBRARIES := xhook

# You can remove this block if you are using NDK r21+.
ifneq ($(call ndk-major-at-least,21),true)
    $(call import-add-path,$(NDK_GRADLE_INJECTED_IMPORT_PATH))
endif

$(call import-module,prefab/xhook)
```

### CMake

```cmake
find_package(xhook REQUIRED CONFIG)
target_link_libraries(<your lib> xhook::xhook)
```