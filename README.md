这是一个练手项目
# 克隆 vcpkg 并构建
git clone https://github.com/microsoft/vcpkg.git
cd vcpkg
.\bootstrap-vcpkg.bat

# 安装项目所需的依赖库
./vcpkg install glfw3 glm imgui

cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE=./vcpkg/scripts/buildsystems/vcpkg.cmake
