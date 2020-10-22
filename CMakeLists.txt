cmake_minimum_required(VERSION 3.7)
project(TF_CPP_DETECT)

set(CMAKE_CXX_STANDARD 14)
ADD_COMPILE_OPTIONS(-fPIC)

set(SOURCE_FILES detect.cpp main.cpp base64.cpp base64.h)
add_executable(tf_detect_crow ${SOURCE_FILES})
SET_TARGET_PROPERTIES(tf_detect_crow PROPERTIES PREFIX "")

# crow lib
#include_directories("/usr/local/include")

# target_compile_definitions(tf_detect_crow PUBLIC "-D_GLIBCXX_USE_CXX11_ABI=0")

# OpenCV libs
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
target_link_libraries(tf_detect_crow ${OpenCV_LIBS})

# boost lib
find_package(Boost REQUIRED COMPONENTS system thread)
include_directories( ${Boost_INCLUDE_DIRS} )
target_link_libraries(tf_detect_crow ${Boost_SYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY})

# use old abi
# add_definitions(-D_GLIBCXX_USE_CXX11_ABI=0)

# pthread link
target_link_libraries(tf_detect_crow -lpthread -lm)
# ==================== PATHS TO SPECIFY! ==================== #

# Eigen lib headers
include_directories("/usr/local/include/eigen3")
include_directories("/usr/local/include/google")

# TensorFlow headers
include_directories("/usr/include/tensorflow/")
include_directories("/usr/include/tensorflow/bazel-genfiles/")
include_directories("/usr/include/tensorflow/")
include_directories("/usr/include/tensorflow/third-party/")

# Link TensorFlow libs
target_link_libraries(tf_detect_crow "/usr/lib/libtensorflow_cc.so")
target_link_libraries(tf_detect_crow "/usr/lib/libtensorflow_framework.so")
