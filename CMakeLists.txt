cmake_minimum_required(VERSION 3.10)
project(FabricCAD3D)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake)

# 设置C++标准
set(CMAKE_CXX_STANDARD 17)

# 包含头文件目录
include_directories(include)

# 设置源文件
file(GLOB_RECURSE SOURCES "src/*.cpp")

# 添加可执行文件
add_executable(FabricCAD3D ${SOURCES})

# 链接 OpenGL 库
find_package(OpenGL REQUIRED)
if(OPENGL_FOUND)
    target_link_libraries(FabricCAD3D PRIVATE OpenGL::GL)
else()
    message(FATAL_ERROR "OpenGL not found")
endif()

# 链接 GLFW 库
find_package(glfw3 CONFIG REQUIRED)
if(glfw3_FOUND)
    target_link_libraries(FabricCAD3D PRIVATE glfw)
else()
    message(FATAL_ERROR "glfw3 not found")
endif()

# 链接 GLM 库
find_package(glm CONFIG REQUIRED)
if(glm_FOUND)
    target_link_libraries(FabricCAD3D PRIVATE glm::glm)
else()
    message(FATAL_ERROR "glm not found")
endif()

# 链接 ImGui 库
find_package(imgui REQUIRED)
if(imgui_FOUND)
    target_link_libraries(FabricCAD3D PRIVATE imgui::imgui)
else()
    message(FATAL_ERROR "imgui not found")
endif()


# 配置编译器选项以支持 UTF-8
if(MSVC)
    add_compile_options(/utf-8)
else()
    add_compile_options(-finput-charset=UTF-8 -fexec-charset=UTF-8)
endif()