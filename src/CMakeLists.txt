add_executable(imgui-example
  main.cpp
)

# Yep, that's it!
target_link_libraries(imgui-example
  PUBLIC
    imgui-sdl
    imgui-opengl3
)

if(WIN32)
  target_link_libraries(imgui-example PUBLIC SDL2main)
  add_custom_command(TARGET imgui-example POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
        $<TARGET_FILE:SDL2>
        $<TARGET_FILE_DIR:imgui-example>)
endif()