cmake_minimum_required(VERSION 3.8)

if(NOT CMAKE_BUILD_TYPE)
set(CMAKE_BUILD_TYPE Release)
endif()
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake ${CMAKE_MODULE_PATH})

project(Sparrow)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS "-Wall -Wextra")
#set(CMAKE_CXX_FLAGS_DEBUG "-g")
#set(CMAKE_CXX_FLAGS_RELEASE "-O3")

#quickjspp support
#add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/deps/quickjspp)

find_package(CURL REQUIRED)
find_package(Threads REQUIRED)
find_package(FLTK REQUIRED)
find_package(litehtml CONFIG REQUIRED)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}/include 
    ${FLTK_INCLUDE_DIRS}
    ${CURL_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty
)

link_libraries(${CURL_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT} ${FLTK_LIBRARIES})

file(GLOB_RECURSE PREON_SRC
${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp
)

add_executable(${PROJECT_NAME} ${PREON_SRC})
