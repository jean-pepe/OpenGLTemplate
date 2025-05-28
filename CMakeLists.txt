cmake_minimum_required(VERSION 3.16)
project(OpenGLTemplate)

set(CMAKE_CXX_STANDARD 17)

# Include subdirs
add_subdirectory(external/spdlog)
add_subdirectory(external/imgui)

# GLAD
add_library(glad STATIC external/glad/src/glad.c)
target_include_directories(glad PUBLIC external/glad/include)

# stb_image
add_library(stb_image STATIC external/stb/stb_image.cpp)
target_include_directories(stb_image PUBLIC external/stb)

# Assimp --> Evita di costruire tool, test, e zlib interno
set(ASSIMP_BUILD_TESTS OFF)
set(ASSIMP_NO_EXPORT ON)
set(ASSIMP_BUILD_ASSIMP_TOOLS OFF)
set(ASSIMP_BUILD_ZLIB ON) # o OFF se vuoi usare lo zlib di sistema
add_subdirectory(external/assimp)

# SDL3
add_subdirectory(external/SDL)
target_link_libraries(OpenGLApp PRIVATE SDL3::SDL3)

# Executable
add_executable(OpenGLApp
    src/main.cpp
)

# Include directories
target_include_directories(OpenGLApp PRIVATE
    external/glad/include
    external/glm
    external/stb
    external/imgui
    ${GLFW_INCLUDE_DIRS}
)

# Link libraries
target_link_libraries(OpenGLApp
    glad
    stb_image
    assimp
    imgui
    spdlog::spdlog
    ${GLFW_LIBRARIES}
    ${CMAKE_DL_LIBS}
)