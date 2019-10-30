cmake_minimum_required (VERSION 3.0) #can prob be less, just from example I was using

set(CMAKE_INCLUDE_CURRENT_DIR ON)

#find_package(Python COMPONENTS Development) #favors python3, then 2...
#FindPython2()
#FindPython3()
find_package(Python3 COMPONENTS Development) #python3 only

add_library(libpicxx
    src/Exception.cxx

    headers/Base.hxx
	headers/ExtModule.hxx
	headers/ExtObj.hxx
	headers/Objects.hxx
	
	headers/Base/Config.h
    headers/Base/Debug.h
    headers/Base/Exception.hxx
    headers/Base/File.h
	
	headers/ExtObj/Bridge.hxx
	headers/ExtObj/ExtObjBase.hxx
	headers/ExtObj/ExtObject.hxx
	headers/ExtObj/FuncMapper.hxx
	headers/ExtObj/NewStyle.hxx
	headers/ExtObj/OldStyle.hxx
	headers/ExtObj/TypeObject.hxx
)

target_include_directories(libpicxx
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/headers
#Interesting, generic python is plural, specific is not...?
#even tho, ('latest') python docs
#(https://cmake.org/cmake/help/latest/module/FindPython3.html) indicate as plural,
#in cmakecache.txt is singular???
	${Python_INCLUDE_DIRS}
	${Python3_INCLUDE_DIR}
)

set_property(TARGET libpicxx PROPERTY CXX_STANDARD 11)
set_property(TARGET libpicxx PROPERTY CXX_EXTENSIONS OFF)
