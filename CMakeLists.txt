cmake_minimum_required(VERSION 2.8)
project(utengine-example)

add_subdirectory(utengine)

find_package(glfw3 3.3 REQUIRED)
find_package(GLEW REQUIRED)
find_package(OpenGL REQUIRED)
find_package(glm REQUIRED)
add_library(SOIL2 STATIC IMPORTED)

if(WIN32)
    set_target_properties(SOIL2 PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/dependencies/SOIL2/soil2.lib)
elseif(UNIX AND NOT APPLE)
    set_target_properties(SOIL2 PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/dependencies/SOIL2/libsoil2.a)
elseif(UNIX AND APPLE)
    # Include apple libs
endif(WIN32)

include_directories(includes/
                    utengine/includes/
                    ${GLEW_INCLUDE_DIRS}
                    ${OPENGL_INCLUDE_DIR}
                    ${GLM_INCLUDE_DIRS}
                    dependencies/SOIL2/includes/)


file(GLOB PROJECT_HEADERS includes/*.h)
file(GLOB PROJECT_SOURCES src/*.cpp)
file(GLOB PROJECT_ASSETS assets/shaders/*.glsl)


source_group("Headers" FILES ${PROJECT_HEADERS})
source_group("Sources" FILES ${PROJECT_SOURCES})
source_group("Assets" FILES ${PROJECT_ASSETS})


add_executable(${PROJECT_NAME} ${PROJECT_SOURCES} ${PROJECT_HEADERS} ${PROJECT_ASSETS})
target_link_libraries(${PROJECT_NAME} GLEW::GLEW
    ${OPENGL_gl_LIBRARY}
    glfw
    utengine
    SOIL2)