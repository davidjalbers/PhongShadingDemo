cmake_minimum_required(VERSION 3.16)
project(PhongShadingDemo)

set(CMAKE_CXX_STANDARD 17)

add_subdirectory(Vendor/GLFW)
add_subdirectory(Vendor/GL3W)
add_subdirectory(Vendor/GLM)

add_executable(PSD
        Source/main.cpp
        Source/Core/Shader.cpp
        Source/Core/Shader.h
        Source/Core/Application.cpp
        Source/Core/Application.h
        Source/Core/VertexArray.cpp
        Source/Core/VertexArray.h
        Source/Core/Input.h
        Source/ControlPanel.cpp
        Source/ControlPanel.h
        Source/PSD.h
        Source/GeometryObject.cpp
        Source/GeometryObject.h
        Source/Camera.cpp
        Source/Camera.h
        Source/Renderer.cpp
        Source/Renderer.h
        Vendor/ImGui/imgui.cpp
        Vendor/ImGui/imgui_draw.cpp
        Vendor/ImGui/imgui_widgets.cpp
        Vendor/ImGui/imgui_demo.cpp
        Vendor/ImGui/backends/imgui_impl_opengl3.cpp
        Vendor/ImGui/backends/imgui_impl_glfw.cpp)

# FIXME Symlinks sind sehr problematisch. Aber copy, copy_if_different und copy_directory übernehmen scheinbar keine Änderungen
add_custom_command(
        TARGET PSD PRE_BUILD
        COMMAND ${CMAKE_COMMAND} -E create_symlink "${CMAKE_SOURCE_DIR}/Resources" "${CMAKE_CURRENT_BINARY_DIR}/Resources"
)
target_include_directories(PSD PRIVATE
        Vendor/ImGui
        Vendor/ImGui/backends)
target_link_libraries(PSD
        gl3w
        glfw
        glm)

