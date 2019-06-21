cmake_minimum_required(VERSION 2.8)
project(utengine)

find_package(glfw3 3.3 REQUIRED)
find_package(GLEW REQUIRED)
find_package(OpenGL REQUIRED)
find_package(glm REQUIRED)

include_directories(includes/
                    ${GLEW_INCLUDE_DIRS}
                    ${OPENGL_INCLUDE_DIR}
                    ${GLM_INCLUDE_DIRS}
                    utengine/includes/)

file(GLOB UTENGINE_HEADERS utengine/includes/*.h)
file(GLOB UTENGINE_SOURCES utengine/src/*.cpp)

source_group("Headers" FILES ${UTENGINE_HEADERS})
source_group("Sources" FILES ${UTENGINE_SOURCES})

add_executable(${PROJECT_NAME} ${UTENGINE_SOURCES} ${UTENGINE_HEADERS})
target_link_libraries(${PROJECT_NAME} ${GLEW_LIBRARIES}
    ${OPENGL_gl_LIBRARY}
    glfw)



project(utengine-example)

file(GLOB PROJECT_HEADERS includes/*.h)
file(GLOB PROJECT_SOURCES src/*.cpp)

source_group("Headers" FILES ${PROJECT_HEADERS})
source_group("Sources" FILES ${PROJECT_SOURCES})

add_executable(${PROJECT_NAME} ${PROJECT_SOURCES} ${PROJECT_HEADERS})
target_link_libraries(${PROJECT_NAME} ${GLEW_LIBRARIES}
    ${OPENGL_gl_LIBRARY}
    glfw)