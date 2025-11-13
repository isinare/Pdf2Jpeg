# 1. Set the minimum CMake version
cmake_minimum_required(VERSION 3.10)

# 2. Name your project
project(converter_engine)

# 3. Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 4. Find the pkg-config tool
find_package(PkgConfig REQUIRED)

# 4a. Manually include the helper file
# This defines the 'pkg_check_modules' command
include(FindPkgConfig)

# 5. Use pkg-config to find "poppler-cpp"
# This creates POPPLER_CPP_INCLUDE_DIRS and POPPLER_CPP_LIBRARIES
pkg_check_modules(POPPLER_CPP REQUIRED poppler-cpp)

# 6. Define our executable
add_executable(converter main.cpp)

# 7. Link Poppler to our executable
# 7a. Tell "converter" where to find Poppler's header files
target_include_directories(converter PRIVATE ${POPPLER_CPP_INCLUDE_DIRS})

# 7b. Tell "converter" which binary files to link
target_link_libraries(converter PRIVATE ${POPPLER_CPP_LIBRARIES})