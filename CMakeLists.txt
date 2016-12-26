cmake_minimum_required(VERSION 3.6)
project(learnopengl)

# Set the name of the ouput binary
set(BIN_NAME "LearnOpenGL")

# Add GLFW
find_package(glfw3 3.2 REQUIRED)

# Add GLEW
find_package(GLEW REQUIRED)
if (GLEW_FOUND)
    include_directories(${GLEW_INCLUDE_DIRS})
    link_libraries(${GLEW_LIBRARIES})
endif()

# Add OpenGL and GLUT
find_package(OpenGL 3.3 REQUIRED)
find_package(GLUT REQUIRED)
include_directories( ${OPENGL_INCLUDE_DIRS}  ${GLUT_INCLUDE_DIRS} )

set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES main.cpp)
add_executable(${BIN_NAME} ${SOURCE_FILES})

target_link_libraries(${BIN_NAME} ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} glfw ${GLEW_LIBRARIES})