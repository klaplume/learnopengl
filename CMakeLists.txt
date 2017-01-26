cmake_minimum_required(VERSION 3.5)
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

set(SOURCE_FILES main.cpp Shader.h Camera.h)
add_executable(${BIN_NAME} ${SOURCE_FILES})

# Add SOIL
# find_package(soil REQUIRED)
target_link_libraries(${BIN_NAME} ${CMAKE_SOURCE_DIR}/lib/libSOIL.a)

# Add GLM
include_directories(${CMAKE_SOURCE_DIR}/lib/glm)

# Copy shaders
configure_file(shaders/default.vert shaders/default.vert COPYONLY)
configure_file(shaders/default.frag shaders/default.frag COPYONLY)
configure_file(shaders/light.frag shaders/light.frag COPYONLY)
# Copy textures
configure_file(textures/wall.jpg textures/wall.jpg COPYONLY)
configure_file(textures/container.jpg textures/container.jpg COPYONLY)
configure_file(textures/awesomeface.png textures/awesomeface.png COPYONLY)

target_link_libraries(${BIN_NAME} ${OPENGL_LIBRARIES} ${GLUT_LIBRARY} glfw ${GLEW_LIBRARIES})
