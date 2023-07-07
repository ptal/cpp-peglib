cmake_minimum_required(VERSION 3.14)
project(cpp-peglib)

if (CMAKE_VERSION VERSION_GREATER_EQUAL "3.24.0")
  cmake_policy(SET CMP0135 NEW)
endif()

add_library(cpp_peglib INTERFACE)
target_include_directories(cpp_peglib INTERFACE ${CMAKE_SOURCE_DIR})
target_compile_features(cpp_peglib INTERFACE cxx_std_20)

option(PEGLIB_BUILD_TESTS "Build cpp-peglib tests" OFF)
option(PEGLIB_BUILD_LINT "Build cpp-peglib lint" OFF)
option(PEGLIB_BUILD_EXAMPLE "Build cpp-peglib example" OFF)

if(${PEGLIB_BUILD_LINT})
  add_subdirectory(lint)
endif()

if(${PEGLIB_BUILD_EXAMPLE})
  add_subdirectory(example)
endif()

if (${PEGLIB_BUILD_TESTS})
  add_subdirectory(test)
  enable_testing()
endif()

install(FILES peglib.h DESTINATION include)
