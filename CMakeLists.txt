cmake_minimum_required(VERSION 2.8)
cmake_policy(SET CMP0015 NEW)

project(JDGO)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/extlibs/find")

add_subdirectory(extlibs/build/TGUI)
add_subdirectory(extlibs/build/vili)

file(GLOB PG_JDGO include/*.hpp)
file(GLOB HD_JDGO src/*.cpp)

if(CMAKE_COMPILER_IS_GNUCC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpermissive -O3")
endif()

set_property(GLOBAL APPEND_STRING PROPERTY COMPILE_FLAGS -Wall)

find_package(SFML 2 REQUIRED graphics window system network audio)

include_directories(include/)
include_directories(extlibs/include/)

include_directories(${SFML_INCLUDE_DIR})

add_executable(JDGO ${PG_JDGO} ${HD_JDGO})

target_link_libraries(JDGO tgui)
target_link_libraries(JDGO vili)

if(SFML_FOUND)
  target_link_libraries(JDGO ${EXECUTABLE_NAME} ${SFML_LIBRARIES})
endif()

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 14)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD_REQUIRED ON)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_EXTENSIONS OFF)