(WIP) Dear ImGui FetchContent example
==========================

This is WIP example of using CMake FetchContent in real world scenario.

It downloads Dear ImGui (my custom CMake branch for now), GLFW and SDL and then a simple application uses these
dependencies for building. Everything is built from source.

**Works on Linux only now**

Building is simple, just do:

```sh
mkdir build
cd build
cmake <path-to-cloned-repo>
cmake --build .
./src/imgui-example
```

You'll also find all the Dear ImGui examples built in `_deps/imgui-build/examples/` directory.

Options
-------

You can also set the following options when building:

* `LINK_DEPS_STATIC` (`OFF` by default) - link dependencies statically

Depencies
---

CMake >= 3.14
