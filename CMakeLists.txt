cmake_minimum_required(VERSION 3.10)
project(submodule-1.1)

enable_testing()

# Create a library that can be linked against
add_library(submodule11_lib submodule11.c)

# Create the executable with a different name
add_executable(submodule11 submodule11.c)

# Add Google Test
find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

# Compile test executable
add_executable(test-submodule11 test-submodule11.cpp)
target_link_libraries(test-submodule11 GTest::GTest GTest::Main pthread submodule11_lib)

# Register test with CTest
add_test(NAME submodule1_1_test COMMAND test-submodule11)

# Make the library target available to parent projects
set_target_properties(submodule11_lib PROPERTIES EXPORT_NAME submodule11_lib)

