cmake_minimum_required(VERSION 3.5.1)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

set(CMAKE_CXX_FLAGS "-Wall -shared")
set (CMAKE_CXX_STANDARD 11)
set(PYBIND11_CPP_STANDARD -std=c++11)
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

project(automated-bar)

#find_library(wiringPi_LIB wiringPi)
#find_library(wiringPi9685_LIB wiringPiPca9685)

include_directories(
		     /usr/include/python3.5m
		     /usr/local/include/python3.5 
		     /home/$ENV{USER}/.local/include/python3.5m
		     ${CMAKE_CURRENT_SOURCE_DIR}/src/pca9685/src
)

add_executable(extension.cpython-35m-arm-linux-gnueabihf.so MultiServoControl.cpp)

target_link_libraries(extension.cpython-35m-arm-linux-gnueabihf.so -lwiringPi) #${wiringPi_LIB})
target_link_libraries(extension.cpython-35m-arm-linux-gnueabihf.so -lwiringPiPca9685) #${wiringPi9685_LIB})
