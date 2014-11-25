cmake_minimum_required(VERSION 2.8)
project(lua_with_cmake C)

if(MSVC)
	#make Visual C++ build in parallel
	add_definitions("/MP")
endif()

add_subdirectory(lua51)
