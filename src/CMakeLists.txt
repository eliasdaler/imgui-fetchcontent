add_executable(imgui-example
  main.cpp
)

# Yep, that's it!
target_link_libraries(imgui-example
  PUBLIC
    imgui-sdl
    imgui-opengl3
)
