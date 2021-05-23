include(FetchContent)

# SDL
FetchContent_Declare(
  SDL
  GIT_REPOSITORY "https://github.com/libsdl-org/SDL"
  GIT_TAG        "release-2.0.14"
)

if(BUILD_SHARED_LIBS)
  set(SDL_SHARED ON CACHE BOOL "Build SDL2 as a shared lib" FORCE)
  set(SDL_STATIC OFF CACHE BOOL "Build SDL2 as a static lib" FORCE)
else()
  set(SDL_SHARED OFF CACHE BOOL "Build SDL2 as a shared lib" FORCE)
  set(SDL_STATIC ON CACHE BOOL "Build SDL2 as a static lib" FORCE)
endif()

FetchContent_MakeAvailable(SDL)

# glew (fork with of glew with CMake build)
# Needed for OpenGL3 loading
FetchContent_Declare(
  glew
  GIT_REPOSITORY "https://github.com/Perlmint/glew-cmake"
  GIT_TAG        "glew-cmake-2.2.0"
)

if(BUILD_SHARED_LIBS)
  set(glew-cmake_BUILD_SHARED ON CACHE BOOL "Build the shared glew library" FORCE)
  set(glew-cmake_BUILD_STATIC OFF CACHE BOOL "Build the static glew library" FORCE)
else()
  set(glew-cmake_BUILD_SHARED OFF CACHE BOOL "Build the shared glew library" FORCE)
  set(glew-cmake_BUILD_STATIC ON CACHE BOOL "Build the static glew library" FORCE)
endif()

FetchContent_MakeAvailable(glew)

# Dear ImGui
FetchContent_Declare(
  imgui
  GIT_REPOSITORY "https://github.com/ocornut/imgui"
  GIT_TAG        "v1.82"
)
FetchContent_MakeAvailable(imgui)

add_library(imgui_sdl
  "${imgui_SOURCE_DIR}/imgui.cpp"
  "${imgui_SOURCE_DIR}/imgui_draw.cpp"
  "${imgui_SOURCE_DIR}/imgui_tables.cpp"
  "${imgui_SOURCE_DIR}/imgui_widgets.cpp"
  # optional
  "${imgui_SOURCE_DIR}/imgui_demo.cpp"
  "${imgui_SOURCE_DIR}/misc/cpp/imgui_stdlib.cpp"
  # SDL + OpenGL3
  "${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp"
  "${imgui_SOURCE_DIR}/backends/imgui_impl_sdl.cpp"
)

target_include_directories(imgui_sdl
  PUBLIC
    "${imgui_SOURCE_DIR}"
    "${imgui_SOURCE_DIR}/backends/"
)

if(BUILD_SHARED_LIBS)
  target_link_libraries(imgui_sdl 
    PUBLIC
      SDL2
      libglew_shared
  )
else()
  target_link_libraries(imgui_sdl 
    PUBLIC
      SDL2-static
      libglew_static
  )
endif()