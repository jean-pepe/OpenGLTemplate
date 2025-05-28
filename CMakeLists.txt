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

# Assimp
set(ASSIMP_BUILD_TESTS OFF)
set(ASSIMP_NO_EXPORT ON)
set(ASSIMP_BUILD_ASSIMP_TOOLS OFF)
set(ASSIMP_BUILD_ZLIB ON)
add_subdirectory(external/assimp)

# SDL3
set(SDL_TEST OFF CACHE BOOL "" FORCE)
set(SDL_INSTALL_TESTS OFF CACHE BOOL "" FORCE)
set(SDL_SHARED OFF CACHE BOOL "" FORCE)
set(SDL_STATIC ON CACHE BOOL "" FORCE)
add_subdirectory(external/SDL)

# Executable (deve venire PRIMA del link e include)
add_executable(OpenGLApp
    src/main.cpp
)

# Include directories (dopo add_executable)
target_include_directories(OpenGLApp PRIVATE
    external/glad/include
    external/glm
    external/stb
    external/imgui
)

# Link libraries (dopo add_executable)
target_link_libraries(OpenGLApp
    glad
    stb_image
    assimp
    imgui
    spdlog::spdlog
    SDL3::SDL3
    ${CMAKE_DL_LIBS}
)
