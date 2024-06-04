cmake_minimum_required(VERSION 3.0)
project(hopf)

# based largely on: 
# https://github.com/Polytonic/Glitter/blob/master/CMakeLists.txt

# turn off compiler warnings
if(MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic -std=c++11")
endif()

# setup GLFW CMake project
add_subdirectory("${PROJECT_SOURCE_DIR}/external/glfw-3.3.8")

# include headers
include_directories("${PROJECT_SOURCE_DIR}/include")
include_directories(/home/shoshin/Downloads/download_gl/glfw-3.3.8/include)
include_directories("${PROJECT_SOURCE_DIR}/external/imgui/include")
include_directories("${PROJECT_SOURCE_DIR}/external/glad/include")
include_directories(/home/shoshin/Downloads/download_gl/glm/glm)
include_directories("${PROJECT_SOURCE_DIR}/external/imgui/include")
file(GLOB PROJECT_HEADERS "include/*.h")

# include source files
file(GLOB PROJECT_SOURCES "src/*.cpp")
file(GLOB IMGUI_SOURCES "external/imgui/src/*.cpp")
file(GLOB GLAD_SOURCES "external/glad/src/*.c")

# group files in IDE
source_group("include" FILES ${PROJECT_HEADERS})
source_group("src" FILES ${PROJECT_SOURCES})
source_group("external" FILES ${IMGUI_SOURCES} ${GLAD_SOURCES})

# create the executable
add_executable(hopf ${PROJECT_SOURCES}
					${PROJECT_HEADERS} # if not included here, it won't show up in the IDE?
					${IMGUI_SOURCES}
					${GLAD_SOURCES})
add_definitions(-DGLEW_STATIC)
# Add OpenGL library and link against it
set(OpenGL_GL_PREFERENCE "GLVND")
find_package(OpenGL REQUIRED)
target_link_libraries(hopf PRIVATE OpenGL::GL)

# add libraries
target_link_libraries(hopf PRIVATE ~/space/__aux/glew-2.1.0/build/build_glew/build_glew/lib/Release/libGLEW.so /home/shoshin/Downloads/build_glfw/src/Release/libglfw.so GL)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
# add libraries
