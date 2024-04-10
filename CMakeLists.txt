cmake_minimum_required(VERSION 3.10)
project(imgui_demo)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

#  define this in case imgui and backends are in a different directory then we can set it here
set(IMGUI_DIR ${CMAKE_SOURCE_DIR})

file(GLOB SOURCES
    "main.cpp"
    "${IMGUI_DIR}/imgui/*.cpp"
    "${IMGUI_DIR}/backends/imgui/*.cpp"
    "${IMGUI_DIR}/backends/*.cpp"
)

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE
    ${IMGUI_DIR}/imgui
    ${IMGUI_DIR}/backends
)

set(glfw3_DIR "/usr/local/Cellar/glfw/3.4")


if(APPLE)
    find_library(COCOA_LIBRARY Cocoa)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(COREVIDEO_LIBRARY CoreVideo)
    find_package(OpenGL REQUIRED)
    find_package(glfw3 REQUIRED)

    target_link_libraries(${PROJECT_NAME} PRIVATE
        ${COCOA_LIBRARY}
        ${IOKIT_LIBRARY}
        ${COREVIDEO_LIBRARY}
        OpenGL::GL
        glfw
    )
endif()