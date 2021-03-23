#(WIP) Dear ImGui FetchContent example

This is WIP example of using CMake FetchContent in real world scenario.

It downloads Dear ImGui (my custom CMake branch for now), GLFW and SDL and then a simple application uses these
dependencies for building. Everything is built from source.

**Works on Windows and Linux only for now**.

Supported implementations:

* SDL (OpenGL2, OpenGL3)
* GLFW (OpenGL2, OpenGL3)

Building is simple, just do:

```sh
git clone https://github.com/eliasdaler/imgui-fetchcontent
mkdir build
cd build
cmake ../https://github.com/eliasdaler/imgui-fetchcontent
cmake --build .
./src/imgui-example # on Windows: .\src\Debug\imgui-example.exe
```

You'll also find all the Dear ImGui examples built in `build/_deps/imgui-build/examples/` directory.

## Options

You can also set the following options when building:

* `LINK_DEPS_STATIC` (`OFF` by default) - link dependencies statically

## Dependencies

CMake >= 3.14

## Notes about Dear ImGui's `cmake` branch

This uses my `cmake` branch of my Dear ImGui's fork. Dear ImGui now also has CMakeLists.txt, so building it with examples is very simple.

If using prebuilt libraries:

```sh
git clone -b cmake https://github.com/eliasdaler/imgui/
mkdir build
cmake ../imgui -DIMGUI_SDL_PREBUILT_DIR=<path-to-SDL-binaries> -DIMGUI_GLFW_PREBUILT_DIR=<path-to-GLFW-binaries>
cmake --build .
```

Note about `IMGUI_SDL_PREBUILT_DIR` and `IMGUI_GLFW_PREBUILT_DIR` - you need to extract the archives and set this variables to a directory where `include` and `lib` directories are.

Building SDL and GLFW manually via CMake and using it for Dear ImGui's build:

```sh
git clone -b cmake https://github.com/eliasdaler/imgui/
mkdir build
cmake ../imgui -DSDL2_DIR=<path-to-SDL2Config.cmake> -Dglfw3_DIR=<path-to-glfw3Config.cmake>
cmake --build .
```

**TODO**: more explanations of how to built SDL and GLFW manually.
