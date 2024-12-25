cmake_minimum_required(VERSION 3.10)

project(Naett_Test C)
set(CMAKE_C_STANDARD 99)

set(CMAKE_BUILD_TYPE "MinSizeRel")

add_executable(${PROJECT_NAME})
target_sources(${PROJECT_NAME} PRIVATE main.c naett/naett.c)

if(CMAKE_SYSTEM_NAME STREQUAL "Windows")
    target_link_libraries(${PROJECT_NAME} PRIVATE winhttp)
elseif(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    find_package(CURL REQUIRED)
    target_link_libraries(${PROJECT_NAME} PRIVATE CURL::libcurl pthread)
elseif(CMAKE_SYSTEM_NAME STREQUAL "Darwin")
    set(CMAKE_EXE_LINKER_FLAGS "-framework Foundation")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-gnu-zero-variadic-macro-arguments")
endif()
