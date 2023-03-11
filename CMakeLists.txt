cmake_minimum_required(VERSION 3.10)
project(libsais LANGUAGES C VERSION 2.7.1)

set(CMAKE_C_STANDARD 99)
set(LIBSAIS_SOURCE_DIR "${PROJECT_SOURCE_DIR}/src")
set(LIBSAIS_INCLUDE_DIR "${PROJECT_SOURCE_DIR}/src")

set(LIBSAIS_SOURCES
    "${LIBSAIS_SOURCE_DIR}/libsais.c"
    "${LIBSAIS_SOURCE_DIR}/libsais.h"
    "${LIBSAIS_SOURCE_DIR}/libsais16.c"
    "${LIBSAIS_SOURCE_DIR}/libsais16.h"
    "${LIBSAIS_SOURCE_DIR}/libsais64.c"
    "${LIBSAIS_SOURCE_DIR}/libsais64.h"
)

add_library(sais STATIC ${LIBSAIS_SOURCES})
add_library(sais::sais ALIAS sais)

find_package(OpenMP)
if(OpenMP_C_FOUND)
    target_link_libraries(sais PRIVATE OpenMP::OpenMP_C)
endif()

target_include_directories(sais PUBLIC ${LIBSAIS_INCLUDE_DIR})
target_compile_options(sais PRIVATE -Wall -Wextra)
