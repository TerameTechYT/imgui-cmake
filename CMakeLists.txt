cmake_minimum_required(VERSION 3.14)

foreach(OUTPUTCONFIG IN LISTS CMAKE_CONFIGURATION_TYPES)
    string(TOUPPER ${OUTPUTCONFIG} OUTPUTCONFIG_UPPER)
    set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${OUTPUTCONFIG_UPPER} ${CMAKE_BINARY_DIR}/bin/${OUTPUTCONFIG})
endforeach()

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_C_STANDARD 23)
set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")

option(IMGUI_ALLEGRO5 OFF)
option(IMGUI_ANDROID OFF)
option(IMGUI_DX9 OFF)
option(IMGUI_DX10 OFF)
option(IMGUI_DX11 OFF)
option(IMGUI_DX12 OFF)
option(IMGUI_GLFW OFF)
option(IMGUI_GLUT OFF)
option(IMGUI_OPENGL2 OFF)
option(IMGUI_OPENGL3 OFF)
option(IMGUI_VULKAN OFF)

project(game LANGUAGES CXX)

add_subdirectory(backends)
add_library(imgui.core STATIC
    "imconfig.h"

    "imgui.h"
    "imgui_internal.h"
    "imgui.cpp"
    "imgui_demo.cpp"
    "imgui_draw.cpp"
    "imgui_tables.cpp"
    "imgui_widgets.cpp"

    "misc/cpp/imgui_stdlib.h"
    "misc/cpp/imgui_stdlib.cpp"
    #"misc/freetype/imgui_freetype.h"
    #"misc/freetype/imgui_freetype.cpp"

    "imstb_rectpack.h"
    "imstb_textedit.h"
    "imstb_truetype.h"
)

target_compile_definitions(imgui.core PRIVATE BUILDING)

add_library(imgui.implot STATIC
    "implot.h"
    "implot.cpp"
    "implot_items.cpp"
    "implot_demo.cpp"

    "implot_internal.h"
)

target_compile_definitions(imgui.implot PRIVATE BUILDING)
