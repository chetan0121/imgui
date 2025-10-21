cmake_minimum_required(VERSION 3.15)
project(imgui_static LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Get imgui dir
set(IMGUI_DIR "${CMAKE_CURRENT_SOURCE_DIR}")

# Create a static library of imgui-lib
add_library(imgui_static STATIC
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
    ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)

# Expose include paths
target_include_directories(imgui_static PUBLIC
    ${IMGUI_DIR}
    ${IMGUI_DIR}/backends
    ${GLFW_DIR}/include   # from main cmake file
)

# Force library output into imgui/bin/
set_target_properties(imgui_static PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${IMGUI_DIR}/bin"
)
