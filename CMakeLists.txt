cmake_minimum_required(VERSION 3.5)

set(ProjectName learn)
project(${ProjectName})

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# FROM QtCreator [Extra configurations]
set("CMAKE_CXX_COMPILER" "E:/Qt/Tools/mingw810_64/bin/g++.exe" CACHE "STRING" "" FORCE)
set("CMAKE_C_COMPILER" "E:/Qt/Tools/mingw810_64/bin/gcc.exe" CACHE "STRING" "" FORCE)
set("CMAKE_PREFIX_PATH" "E:/Qt/5.15.0/mingw81_64" CACHE "STRING" "" FORCE)
set("QT_QMAKE_EXECUTABLE" "E:/Qt/5.15.0/mingw81_64/bin/qmake.exe" CACHE "STRING" "" FORCE)

# QtCreator supports the following variables for Android, which are identical to qmake Android variables.
# Check http://doc.qt.io/qt-5/deployment-android.html for more information.
# They need to be set before the find_package(Qt5 ...) call.

#if(ANDROID)
#    set(ANDROID_PACKAGE_SOURCE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/android")
#    if (ANDROID_ABI STREQUAL "armeabi-v7a")
#        set(ANDROID_EXTRA_LIBS
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libcrypto.so
#            ${CMAKE_CURRENT_SOURCE_DIR}/path/to/libssl.so)
#    endif()
#endif()

# fetching all filenames from src & includes directory.
file(GLOB_RECURSE SOURCES 
  includes/*.h
  src/*.cpp
)

find_package(Qt5 COMPONENTS Widgets REQUIRED)

if(ANDROID)
  add_library(${ProjectName} SHARED
    main.cpp
    ${SOURCES}
  )
else()
  add_executable(${ProjectName}
    main.cpp
    ${SOURCES}
  )
endif()

# include file directory
target_include_directories(${ProjectName} PRIVATE includes)
# 
target_link_libraries(${ProjectName} PRIVATE Qt5::Widgets)
