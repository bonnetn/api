cmake_minimum_required(VERSION 3.7)
project(facade)

find_package(cpprestsdk REQUIRED)

add_executable(facade src/main.cpp)
target_link_libraries(facade PRIVATE cpprestsdk::cpprest)
