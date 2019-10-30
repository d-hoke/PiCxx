cmake_minimum_required (VERSION 3.0) #can prob be less, just from example I was using


set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Python3 COMPONENTS Development) #python3 only
#link_directories(${Python3_LIBRARY_DIRS})
link_directories(${Python3_LIBRARY_DIR})

message(STATUS "python3 lib dir ${Python3_LIBRARY_DIR}#${Python3_LIBRARY_DIRS}")

add_executable(test-PiCxx
    main.cpp
	test_objects.cxx
	test_funcmapper.cxx
	test_prompt.cxx
	# test_funcmapper.py - what to do with this,where/how/what
)

target_link_libraries(test-PiCxx PUBLIC
    libpicxx
	${Python3_LIBRARIES}
)

set_property(TARGET test-PiCxx PROPERTY CXX_STANDARD 14)
set_property(TARGET test-PiCxx PROPERTY CXX_EXTENSIONS OFF)
