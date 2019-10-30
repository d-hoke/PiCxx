cmake_minimum_required (VERSION 3.0) #can prob be less, just from example I was using


set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Python3 COMPONENTS Development) #python3 only
#link_directories(${Python3_LIBRARY_DIRS})
link_directories(${Python3_LIBRARY_DIR})

message(STATUS "python3 lib dir ${Python3_LIBRARY_DIR}#${Python3_LIBRARY_DIRS}")

add_executable(test_PiCxx
    main.cpp
	test_objects.cxx
	test_funcmapper.cxx
	test_prompt.cxx
	# test_funcmapper.py - what to do with this,where/how/what
)

target_link_libraries(test_PiCxx PUBLIC
    libpicxx
	${Python3_LIBRARIES}
)

set_property(TARGET test_PiCxx PROPERTY CXX_STANDARD 14)
set_property(TARGET test_PiCxx PROPERTY CXX_EXTENSIONS OFF)

#*bomb*
#get_property(test_PiCxx_location TARGET test_PiCxx PROPERTY LOCATION)
#message( "test_PiCxx_location == ${test_PiCxx_location}")

file(TO_NATIVE_PATH ${CMAKE_BINARY_DIR}/py FP1)
file(TO_NATIVE_PATH ${CMAKE_CURRENT_BINARY_DIR}/py FP2)
#file(TO_NATIVE_PATH ${CMAKE_SOURCE_DIR}/test-PiCxx/test_funcmapper.py FP3)
file(TO_NATIVE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/test_funcmapper.py FP3)
file(TO_NATIVE_PATH ${CMAKE_CURRENT_BINARY_DIR}/py/test_funcmapper.py FP4)
#file(TO_NATIVE_PATH ${CMAKE_BINARY_DIR}/py/test_funcmapper.py FP5)
file(TO_NATIVE_PATH ${CMAKE_CURRENT_BINARY_DIR}/py/test_funcmapper.py FP5)
file(TO_NATIVE_PATH ${CMAKE_CURRENT_BINARY_DIR}/$<TARGET_FILE:test_PiCxx> TGTEXECPATH)
add_custom_command(
#    TARGET PiCxx POST_BUILD
    TARGET test_PiCxx POST_BUILD
#	COMMAND mkdir /p ${CMAKE_BINARY_DIR}/py
#	COMMAND mkdir /p ${CMAKE_CURRENT_BINARY_DIR}/py
#	COMMAND mkdir /p ${FP1}
#	COMMAND mkdir /p ${FP2}
	COMMAND ${CMAKE_COMMAND} -E copy
	        "${FP3}" #${CMAKE_SOURCE_DIR}/test_PiCxx/test_funcmapper.py
#			"${FP4}" #${CMAKE_CURRENT_BINARY_DIR}/py/test_funcmapper.py
			"${FP5}" #${CMAKE_CURRENT_BINARY_DIR}/py/test_funcmapper.py
#			"${FP4}" #${CMAKE_BINARY_DIR}/py/test_funcmapper.py
    COMMAND ${TGTEXECPATH}
)
