# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

cmake_minimum_required(VERSION 3.22.1)

project("nativexr")

# Creates your game shared library. The name must be the same as the
# one used for loading in your Kotlin/Java or AndroidManifest.txt files.
add_library(nativexr SHARED
        main.cpp
        AndroidOut.cpp
        Renderer.cpp
        Shader.cpp
        TextureAsset.cpp
        Utility.cpp)

# Searches for a package provided by the game activity dependency
find_package(game-activity REQUIRED CONFIG)

target_include_directories(nativexr PUBLIC
        ${OPENXR_ROOT}/Include)
target_link_directories(nativexr PUBLIC
        ${OPENXR_ROOT}/Libs/Android/${CMAKE_ANDROID_ARCH_ABI}/${CMAKE_BUILD_TYPE})
# Configure libraries CMake uses to link your target library.
target_link_libraries(nativexr
        game-activity::game-activity_static
        openxr_loader
        EGL
        GLESv3
        jnigraphics
        android
        log)