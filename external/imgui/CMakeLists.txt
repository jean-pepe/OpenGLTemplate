file(GLOB IMGUI_SOURCES
    "*.cpp"
    "backends/imgui_impl_sdl3.cpp"
    "backends/imgui_impl_opengl3.cpp"
)

add_library(imgui STATIC ${IMGUI_SOURCES})
target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)
