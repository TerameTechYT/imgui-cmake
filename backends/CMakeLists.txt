cmake_minimum_required(VERSION 3.14)

if(IMGUI_ALLEGRO5)
    add_library(imgui.backends.allegro5 STATIC
        "imgui_impl_allego5.h"
        "imgui_impl_allego5.cpp"
    )

    target_link_libraries(imgui.backends.allegro5 PUBLIC imgui.core)
    target_include_directories(imgui.backends.allegro5 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_ANDROID)
    add_library(imgui.backends.android STATIC
        "imgui_impl_android.h"
        "imgui_impl_android.cpp"
    )

    target_link_libraries(imgui.backends.android PUBLIC imgui.core)
    target_include_directories(imgui.backends.android PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_DX9)
    add_library(imgui.backends.dx9 STATIC
        "imgui_impl_dx9.h"
        "imgui_impl_dx9.cpp"
    )

    target_link_libraries(imgui.backends.dx9 PUBLIC imgui.core)
    target_include_directories(imgui.backends.dx9 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_DX10)
    add_library(imgui.backends.dx10 STATIC
        "imgui_impl_dx10.h"
        "imgui_impl_dx10.cpp"
    )

    target_link_libraries(imgui.backends.dx10 PUBLIC imgui.core)
    target_include_directories(imgui.backends.dx10 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_DX11)
    add_library(imgui.backends.dx11 STATIC
        "imgui_impl_dx11.h"
        "imgui_impl_dx11.cpp"
    )

    target_link_libraries(imgui.backends.dx11 PUBLIC imgui.core)
    target_include_directories(imgui.backends.dx11 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_DX12)
    add_library(imgui.backends.dx12 STATIC
        "imgui_impl_dx12.h"
        "imgui_impl_dx12.cpp"
    )
    target_link_libraries(imgui.backends.dx12 PUBLIC imgui.core)
    target_include_directories(imgui.backends.dx12 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_GLFW)
    add_library(imgui.backends.glfw STATIC
        "imgui_impl_glfw.h"
        "imgui_impl_glfw.cpp"
    )

    find_package(Vulkan REQUIRED)
    find_package(OpenGL REQUIRED)

    target_link_libraries(imgui.backends.glfw PUBLIC imgui.core)
    target_include_directories(imgui.backends.glfw PUBLIC ${CMAKE_SOURCE_DIR})

    ##--  OPENGL + VULKAN
    target_link_libraries(imgui.backends.glfw PUBLIC OpenGL::GL ${Vulkan_LIBRARIES})
    target_include_directories(imgui.backends.glfw PUBLIC ${Vulkan_INCLUDE_DIRS})

    ##-- GLFW
    target_link_libraries(imgui.backends.glfw PUBLIC glfw)
    target_include_directories(imgui.backends.glfw PUBLIC ${glfw_SOURCE_DIR}/include)
endif()

if(IMGUI_GLUT)
    add_library(imgui.backends.glut STATIC
        "imgui_impl_glut.h"
        "imgui_impl_glut.cpp"
    )

    find_package(Vulkan REQUIRED)
    find_package(OpenGL REQUIRED)

    target_link_libraries(imgui.backends.glut PUBLIC imgui.core)
    target_include_directories(imgui.backends.glut PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_OPENGL2)
    add_library(imgui.backends.opengl2 STATIC
        "imgui_impl_opengl2.h"
        "imgui_impl_opengl2.cpp"
    )

    find_package(OpenGL REQUIRED)

    target_link_libraries(imgui.backends.opengl2 PUBLIC imgui.core)
    target_include_directories(imgui.backends.opengl2 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_OPENGL3)
    add_library(imgui.backends.opengl3 STATIC
        "imgui_impl_opengl3.h"
        "imgui_impl_opengl3.cpp"
    )

    find_package(OpenGL REQUIRED)

    target_link_libraries(imgui.backends.opengl3 PUBLIC imgui.core)
    target_include_directories(imgui.backends.opengl3 PUBLIC ${CMAKE_SOURCE_DIR})
endif()

if(IMGUI_VULKAN)
    add_library(imgui.backends.vulkan STATIC
        "imgui_impl_vulkan.h"
        "imgui_impl_vulkan.cpp"
    )

    find_package(Vulkan REQUIRED)

    target_link_libraries(imgui.backends.vulkan PUBLIC imgui.core)
    target_include_directories(imgui.backends.vulkan PUBLIC ${CMAKE_SOURCE_DIR})

    ##--  VULKAN
    target_link_libraries(imgui.backends.vulkan PUBLIC ${Vulkan_LIBRARIES})
    target_include_directories(imgui.backends.vulkan PUBLIC ${Vulkan_INCLUDE_DIRS})
endif()
