cmake_minimum_required (VERSION 3.0) #can prob be less, just from example I was using

project(PiCxx CXX)

enable_testing()

add_subdirectory(PiCxx)
add_subdirectory(test_PiCxx)
