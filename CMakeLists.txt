cmake_minimum_required(VERSION 3.26)

project(ECS-Engine-Sandbox-SDL2-ImGui- LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# ------------------ Dependencies (vcpkg) ------------------
find_package(SDL2 CONFIG REQUIRED)
find_package(SDL2_image CONFIG REQUIRED)
find_package(SDL2_mixer CONFIG REQUIRED)
find_package(SDL2_ttf CONFIG REQUIRED)


# ------------------ ImGui Library ------------------
add_library(imgui STATIC
    External/imgui/imgui.cpp
    External/imgui/imgui_draw.cpp
    External/imgui/imgui_tables.cpp
    External/imgui/imgui_widgets.cpp
    External/imgui/imgui_demo.cpp
    External/imgui/backends/imgui_impl_sdl2.cpp
    External/imgui/backends/imgui_impl_sdlrenderer2.cpp
)

target_include_directories(imgui PUBLIC
    External
    External/imgui
)

# ImGui backend needs SDL
target_link_libraries(imgui PUBLIC SDL2::SDL2)

# ---------------- Game ----------------
add_executable(ECS-Engine-Sandbox-SDL2-ImGui-
    src/main.cpp
    src/Action.cpp
    src/ActionManager.cpp
    src/AssetManager.cpp
    src/AudioSystem.cpp
    src/Collision.cpp
    src/EntityManager.cpp
    src/Game.cpp
    src/Gui.cpp
    src/Input.cpp
    src/LivesSystem.cpp
    src/MovementSystem.cpp
    src/Music.cpp
    src/PhysicsSystem.cpp
    src/Renderer.cpp
    src/RenderSystem.cpp
    src/SceneGame.cpp
    src/ScoreSystem.cpp
    src/Sound.cpp
    src/Text.cpp
    src/Texture.cpp
    src/Timer.cpp
    src/Window.cpp
    src/SceneStart.cpp
    src/SceneRestart.cpp
    src/VertexArray.cpp
)

target_include_directories(ECS-Engine-Sandbox-SDL2-ImGui- PRIVATE
    include
    
)



target_link_libraries(ECS-Engine-Sandbox-SDL2-ImGui- PRIVATE
    imgui
    SDL2::SDL2
    SDL2_image::SDL2_image
    SDL2_mixer::SDL2_mixer
    SDL2_ttf::SDL2_ttf
)

# ---------------- Assets ----------------
add_custom_target(copy_assets ALL
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/assets
        $<TARGET_FILE_DIR:ECS-Engine-Sandbox-SDL2-ImGui->/assets
)
add_dependencies(ECS-Engine-Sandbox-SDL2-ImGui- copy_assets)
