cmake_minimum_required(VERSION 3.10)
project(RawGLFWProject)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)

# Add GLFW
add_subdirectory(third_party/glfw)

# Add GLAD
add_library(glad STATIC third_party/glad/src/glad.c)
target_include_directories(glad PUBLIC third_party/glad/include)

# Include ImGui
add_library(imgui STATIC
    third_party/imgui/imgui.cpp
    third_party/imgui/imgui_demo.cpp
    third_party/imgui/imgui_draw.cpp
    third_party/imgui/imgui_tables.cpp
    third_party/imgui/imgui_widgets.cpp
    third_party/imgui/backends/imgui_impl_glfw.cpp
    third_party/imgui/backends/imgui_impl_opengl3.cpp
)
# Add include directories for ImGui
target_include_directories(imgui PUBLIC 
    third_party/imgui 
    third_party/imgui/backends 
    third_party/glfw/include
)

# Add source files
file(GLOB SRC_FILES src/*.cpp)

# Add executable
add_executable(mold ${SRC_FILES})

# Link libraries
target_link_libraries(mold PRIVATE glad glfw imgui)

# Include directories
target_include_directories(mold PRIVATE
    third_party/glfw/include
    third_party/imgui
    third_party/glad/include
)
