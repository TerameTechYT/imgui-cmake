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
add_subdirectory(misc)

include(FetchContent)
FetchContent_Declare(glfw GIT_REPOSITORY https://github.com/glfw/glfw.git GIT_TAG master)
FetchContent_MakeAvailable(glfw)

FetchContent_Declare(sdl GIT_REPOSITORY https://github.com/libsdl-org/SDL GIT_TAG main)
FetchContent_MakeAvailable(sdl)

add_library(imgui.core SHARED
    "imconfig.h"

    "imgui.h"
    "imgui_internal.h"
    "imgui.cpp"
    "imgui_demo.cpp"
    "imgui_draw.cpp"
    "imgui_tables.cpp"
    "imgui_widgets.cpp"
    "imgui_widgets.cpp"

    "imstb_rectpack.h"
    "imstb_textedit.h"
    "imstb_truetype.h"
)

find_package(Vulkan REQUIRED)
find_package(OpenGL REQUIRED)
target_include_directories(imgui.core PUBLIC ${glfw_SOURCE_DIR}/include)
target_include_directories(imgui.core PUBLIC ${sdl_SOURCE_DIR}/include)
target_include_directories(imgui.core PUBLIC ${Vulkan_INCLUDE_DIRS})
target_link_libraries(imgui.core PUBLIC OpenGL::GL glfw SDL3-static ${Vulkan_LIBRARIES})
target_compile_definitions(imgui.core PUBLIC BUILDING)
