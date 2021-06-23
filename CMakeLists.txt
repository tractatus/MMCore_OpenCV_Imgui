cmake_minimum_required( VERSION 3.6 )

set( CMAKE_CXX_STANDARD 11 )
set(CMAKE_CXX_FLAGS "-framework Cocoa -framework OpenGL -framework IOKit -framework CoreVideo")

set( CMAKE_CXX_STANDARD_REQUIRED ON )
set( CMAKE_CXX_EXTENSIONS OFF )

find_package( Git )
execute_process(
  COMMAND ${GIT_EXECUTABLE} clone "https://github.com/ocornut/imgui.git"
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)
set( IMGUI_DIR ${CMAKE_CURRENT_BINARY_DIR}/imgui )


set( imgui_files
  ${IMGUI_DIR}/imconfig.h
  ${IMGUI_DIR}/imgui.cpp
  ${IMGUI_DIR}/imgui.h
  ${IMGUI_DIR}/imgui_demo.cpp
  ${IMGUI_DIR}/imgui_draw.cpp
  ${IMGUI_DIR}/imgui_internal.h
  ${IMGUI_DIR}/imgui_tables.cpp
  ${IMGUI_DIR}/imgui_widgets.cpp
  ${IMGUI_DIR}/imstb_rectpack.h
  ${IMGUI_DIR}/imstb_textedit.h
  ${IMGUI_DIR}/imstb_truetype.h
)

set( imgui_impl_files
  ${IMGUI_DIR}/backends/imgui_impl_glfw.h
  ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
  ${IMGUI_DIR}/backends/imgui_impl_opengl3.h
  ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)

set( gl3w
  ${IMGUI_DIR}/examples/libs/gl3w/GL/gl3w.c
)

project( sample )
add_executable( sample ${imgui_files} ${imgui_impl_files} ${gl3w} main.cpp )

set_property( DIRECTORY PROPERTY VS_STARTUP_PROJECT "sample" )

find_package( OpenCV REQUIRED )
find_package( OpenGL REQUIRED )
# glfw
find_package(glfw3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})
link_libraries(${GLFW_LIBRARY_DIRS})

# glew
find_package(GLEW REQUIRED)
include_directories(${GLEW_INCLUDE_DIRS})
link_libraries(${GLEW_LIBRARIES})
find_package(Boost COMPONENTS thread REQUIRED)


if( OpenCV_FOUND AND OPENGL_FOUND )
  include_directories( ${IMGUI_DIR} )
  include_directories( ${IMGUI_DIR}/backends )
  include_directories( ${IMGUI_DIR}/examples )
  include_directories( ${IMGUI_DIR}/examples/libs/gl3w )
  include_directories( ${OPENGL_INCLUDE_DIR} )

  include_directories(${GLFW_INCLUDE_DIRS})

  target_link_libraries( sample ${OpenCV_LIBS} )
  target_link_libraries( sample ${OPENGL_LIBRARIES} )
  target_link_libraries( sample glfw)
  target_link_libraries( sample GLEW::GLEW)
  target_link_libraries(sample Boost::thread)

  target_link_libraries(sample ${CMAKE_SOURCE_DIR}/MMCore/.libs/libMMCore.a)

endif()
