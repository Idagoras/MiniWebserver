cmake_minimum_required(VERSION 3.14)

project(MiniWebserver)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

include(FetchContent)
FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG release-1.12.1
)

FetchContent_MakeAvailable(googletest)

aux_source_directory(src SRCS)

add_executable(logTest ${PROJECT_SOURCE_DIR}/tests/test_log.cpp)

target_include_directories(logTest PRIVATE 
    ${PROJECT_SOURCE_DIR}/include
    ${googletest_SOURCE_DIR}/googletest/include
)
target_link_libraries(logTest PRIVATE gtest_main)

include(GoogleTest)
gtest_discover_tests(logTest)