cmake_minimum_required(VERSION 3.5)
project(wiz_viewer_app)

set (CMAKE_CXX_STANDARD 17)

add_subdirectory(deps/SDL2 EXCLUDE_FROM_ALL)

# Create your game executable target as usual
add_executable(wiz_viewer_app src/main.cpp)

# Link to the actual SDL2 library.
target_link_libraries(wiz_viewer_app PRIVATE SDL3::SDL3)

# Link Mac requirements
find_library(METAL Metal)
find_library(FOUNDATION Foundation)
find_library(QUARTZCORE QuartzCore)

target_link_libraries(wiz_viewer_app PRIVATE stdc++ "-framework Metal" "-framework Foundation" "-framework QuartzCore" objc)

# Include metal-cpp headers
target_include_directories(wiz_viewer_app PRIVATE deps/metal-cpp)
