cmake_minimum_required(VERSION 2.8)

project(usb4java C)
set(PROJECT_VERSION 1.3.1)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/.cmake/Modules/")

set(JAVA_AWT_LIBRARY NotNeeded)
set(JAVA_JVM_LIBRARY NotNeeded)
set(JAVA_INCLUDE_PATH2 NotNeeded)
set(JAVA_AWT_INCLUDE_PATH NotNeeded)

set(LibUsb_LIBRARIES libusblib)
set(LibUsb_INCLUDE_DIRS "${CMAKE_SOURCE_DIR}/../libusb/src/main/cpp/libusb")

add_library(${LibUsb_LIBRARIES} SHARED IMPORTED)

set_target_properties(${LibUsb_LIBRARIES} PROPERTIES IMPORTED_LOCATION
${CMAKE_SOURCE_DIR}/../libusb/build/intermediates/ndkBuild/${CMAKE_BUILD_TYPE}/obj/local/${ANDROID_ABI}/libusb1.0.so)

find_package(JNI REQUIRED)
find_package(LibUsb REQUIRED)

include_directories(${JNI_INCLUDE_DIRS})
include_directories(${LibUsb_INCLUDE_DIRS})

if(CMAKE_COMPILER_IS_GNUCC)
    add_definitions(-Wall -Werror -std=c99)
endif()

add_subdirectory(src)
