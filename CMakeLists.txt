cmake_minimum_required(VERSION 3.5)
project(wiz_viewer_app)

set(CMAKE_CXX_STANDARD 17)
#enable_language(OBJCXX)

add_subdirectory(deps/SDL2 EXCLUDE_FROM_ALL)

# Create your game executable target as usual
add_executable(wiz_viewer_app
    src/main.cpp
    deps/imgui/imgui.cpp
    deps/imgui/imgui_draw.cpp
    deps/imgui/imgui_widgets.cpp
    deps/imgui/imgui_tables.cpp
    deps/imgui/imgui_demo.cpp
    deps/imgui/backends/imgui_impl_metal.mm
    deps/imgui/backends/imgui_impl_sdl2.cpp
)

# Link Mac requirements
find_library(METAL Metal)
find_library(FOUNDATION Foundation)
find_library(QUARTZCORE QuartzCore)

target_link_libraries(wiz_viewer_app PRIVATE
    SDL2::SDL2
    "-framework Metal"
    "-framework Foundation"
    "-framework QuartzCore"
)

# Include metal-cpp headers
target_include_directories(wiz_viewer_app PRIVATE deps/metal-cpp)

# Include imgui headers
target_include_directories(wiz_viewer_app PRIVATE deps/imgui)
target_include_directories(wiz_viewer_app PRIVATE deps/imgui/backends)

# Imgui config
add_compile_definitions(IMGUI_USER_CONFIG="my_imconfig.h")
