# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

#//设置目录，会出现一个问题 More than one file was found with OS independent path 'lib/x86/liblame_3.100.so'
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI})
# 问题：More than one file was found with OS independent path 'lib/x86/liblame_3.100.so'
# 1.判断有文件夹就不编译了
#   File file = file('src/main/jniLibs')
#   //todo 这里的判断可能会不准
#   if (!file.exists() || file.list().size()<=0){
#       cmake {
#           path "CMakeLists.txt"
#       }
#   }
# 2.让他编译，但取第一个文件
#   packagingOptions {
#        pickFirst 'lib/armeabi-v7a/liblame_3.100.so'
#        pickFirst 'lib/armeabi-v8a/liblame_3.100.so'
#        pickFirst 'lib/arm64-v8a/liblame_3.100.so'
#        pickFirst 'lib/x86/liblame_3.100.so'
#        pickFirst 'lib/x86_64/liblame_3.100.so'
#    }

add_library( # Sets the name of the library.
        lame_3.100

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        src/main/cpp/lame_3.100/vector/lame_intrin.h
        src/main/cpp/lame_3.100/vector/xmm_quantize_sub.c
        src/main/cpp/lame_3.100/bitstream.c
        src/main/cpp/lame_3.100/bitstream.h
        src/main/cpp/lame_3.100/encoder.c
        src/main/cpp/lame_3.100/encoder.h
        src/main/cpp/lame_3.100/fft.c
        src/main/cpp/lame_3.100/fft.h
        src/main/cpp/lame_3.100/gain_analysis.c
        src/main/cpp/lame_3.100/gain_analysis.h
        src/main/cpp/lame_3.100/id3tag.c
        src/main/cpp/lame_3.100/id3tag.h
        src/main/cpp/lame_3.100/l3side.h
        src/main/cpp/lame_3.100/lame-analysis.h
        src/main/cpp/lame_3.100/lame.c
        src/main/cpp/lame_3.100/lame.h
        src/main/cpp/lame_3.100/lame_global_flags.h
        src/main/cpp/lame_3.100/lameerror.h
        src/main/cpp/lame_3.100/machine.h
        src/main/cpp/lame_3.100/mpglib_interface.c
        src/main/cpp/lame_3.100/newmdct.c
        src/main/cpp/lame_3.100/newmdct.h
        src/main/cpp/lame_3.100/presets.c
        src/main/cpp/lame_3.100/psymodel.c
        src/main/cpp/lame_3.100/psymodel.h
        src/main/cpp/lame_3.100/quantize.c
        src/main/cpp/lame_3.100/quantize.h
        src/main/cpp/lame_3.100/quantize_pvt.c
        src/main/cpp/lame_3.100/quantize_pvt.h
        src/main/cpp/lame_3.100/reservoir.c
        src/main/cpp/lame_3.100/reservoir.h
        src/main/cpp/lame_3.100/set_get.c
        src/main/cpp/lame_3.100/set_get.h
        src/main/cpp/lame_3.100/tables.c
        src/main/cpp/lame_3.100/tables.h
        src/main/cpp/lame_3.100/takehiro.c
        src/main/cpp/lame_3.100/util.c
        src/main/cpp/lame_3.100/util.h
        src/main/cpp/lame_3.100/vbrquantize.c
        src/main/cpp/lame_3.100/vbrquantize.h
        src/main/cpp/lame_3.100/VbrTag.c
        src/main/cpp/lame_3.100/VbrTag.h
        src/main/cpp/lame_3.100/version.c
        src/main/cpp/lame_3.100/version.h)

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        lame_3.100

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})