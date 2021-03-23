include(FetchContent)

option(LINK_DEPS_STATIC CACHE OFF)

# Don't build shared libs if we want to link to deps statically
if(LINK_DEPS_STATIC)
  set(BUILD_SHARED_LIBS OFF)
else()
  set(BUILD_SHARED_LIBS ON)
endif()

#======================================
FetchContent_Declare(
  imgui
  GIT_REPOSITORY "https://github.com/eliasdaler/imgui"
  GIT_TAG bec4c2fe4c3456c0dafb292da2883c9cf2bc8313
)

FetchContent_Declare(
  SDL
  GIT_REPOSITORY "https://github.com/libsdl-org/SDL"
  GIT_TAG        "release-2.0.14"
)

FetchContent_Declare(
  glfw
  GIT_REPOSITORY "https://github.com/glfw/glfw"
  GIT_TAG        "3.3.3"
)
#======================================

# GLFW
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
FetchContent_MakeAvailable(glfw)

# SDL
if (LINK_DEPS_STATIC)
  set(SDL_STATIC ON CACHE BOOL "Build SDL2 as shared lib")
else()
  set(SDL_SHARED ON CACHE BOOL "Build SDL2 as shared lib")
endif()

FetchContent_MakeAvailable(SDL)

# Define alias for what we used
if (LINK_DEPS_STATIC)
  add_library(SDL2::SDL2 ALIAS SDL2-static)
else()
  add_library(SDL2::SDL2 ALIAS SDL2)
endif()

# Need to be called last so that all 3rd party dependencies are fetched
FetchContent_MakeAvailable(imgui)
