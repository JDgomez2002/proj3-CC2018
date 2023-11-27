cmake_minimum_required(VERSION 3.22)

project(GAME)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pg")

# Find SDL2
find_package(SDL2 REQUIRED)
include_directories(${SDL2_INCLUDE_DIRS})

set(SDL2_image_DIR "/usr/lib/x86_64-linux-gnu/libSDL2_image-2.0.so")

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS
    "${PROJECT_SOURCE_DIR}/src/*.cpp"
)

add_executable(${PROJECT_NAME}
    src/main.cpp
    ${SOURCES}
)

target_include_directories(${PROJECT_NAME}
    PRIVATE ${PROJECT_SOURCE_DIR}/include
    PUBLIC ${PROJECT_SOURCE_DIR}/src
    PUBLIC /usr/lib/x86_64-linux-gnu/libSDL2_image-2.0.so
    PUBLIC /usr/include/glm/glm.hpp
)

target_link_libraries(${PROJECT_NAME}
    ${SDL2_LIBRARIES}
    ${SDL2_image_DIR}
)
