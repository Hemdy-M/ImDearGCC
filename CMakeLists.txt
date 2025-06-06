cmake_minimum_required(VERSION 3.10)
project(DearImGCC)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# === ImGui sources ===
set(IMGUI_DIR ${CMAKE_SOURCE_DIR}/libs/imgui)
set(IMGUI_BACKENDS ${IMGUI_DIR}/backends)

set(IMGUI_SOURCES
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/imgui_stdlib.cpp
    ${IMGUI_BACKENDS}/imgui_impl_glfw.cpp
    ${IMGUI_BACKENDS}/imgui_impl_opengl3.cpp
)

# === GLFW from source ===
add_subdirectory(libs/glfw)
include_directories(libs/glfw/include)

# === Includes ===
include_directories(
    inc
    inc/ui
    inc/core
    ${IMGUI_DIR}
    ${IMGUI_BACKENDS}
)

# === Add executable ===
add_executable(${PROJECT_NAME}
    src/main.cpp
    src/window.cpp
    src/core/compiler.cpp
    src/ui/fileExplorer.cpp
    src/ui/compiler_ui.cpp
    ${IMGUI_SOURCES}
)

# === OpenGL ===
find_package(OpenGL REQUIRED)

# === Link libraries ===
target_link_libraries(${PROJECT_NAME}
    glfw
    OpenGL::GL
)
