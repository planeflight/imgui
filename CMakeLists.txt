cmake_minimum_required(VERSION 3.2)

project(imgui)

set (CMAKE_CXX_FLAGS "-std=c++20")

add_library(${PROJECT_NAME} SHARED
    # imgui
    imconfig.h
    imgui.cpp
    imgui.h
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_impl_opengl3.cpp
    imgui_impl_opengl3.h
    imgui_impl_opengl3_loader.h
    imgui_impl_sdl3.cpp
    imgui_impl_sdl3.h
    imgui_internal.h
    imgui_tables.cpp
    imgui_widgets.cpp
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h

    # implot
    implot.cpp
    implot.h
    implot_demo.cpp
    implot_internal.h
    implot_items.cpp
)

# WARN: A slightly dirty hack to get imgui to link with SDL
option(IMGUI_STANDALONE "Build ImGui as a standalone project" OFF)
if (IMGUI_STANDALONE)
    message("ImGui Standalone build not yet configured.")
else()
    target_link_directories(${PROJECT_NAME} PRIVATE ..)
    target_link_libraries(${PROJECT_NAME} PRIVATE SDL3::SDL3)

    target_include_directories(${PROJECT_NAME} PRIVATE ../SDL/include/)
endif()
