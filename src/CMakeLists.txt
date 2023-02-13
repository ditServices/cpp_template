cmake_minimum_required(VERSION 3.13.4)
project(my_project VERSION 1.0)
set(CMAKE_CXX_STANDARD 17)

# RENAME AS APPROPRIATE
configure_file(../projectConfig.h.in projectConfig.h)

add_executable(${PROJECT_NAME} main.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC ${PROJECT_BINARY_DIR})