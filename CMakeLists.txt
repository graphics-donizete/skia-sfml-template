cmake_minimum_required(VERSION 3.10.0)
project(skia-sfml-template VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 17)
include(FetchContent)

add_executable(skia-sfml-template main.cpp)

FetchContent_Declare(
    sfml
    GIT_REPOSITORY https://github.com/SFML/SFML
    GIT_TAG master
)

FetchContent_MakeAvailable(
    sfml
)

target_link_libraries(
    skia-sfml-template
    PUBLIC
    SFML::Graphics
)

target_include_directories(
    skia-sfml-template
    PUBLIC
    ${CMAKE_SOURCE_DIR}/external/
    ${CMAKE_SOURCE_DIR}/external/skia
)

target_link_libraries(
    skia-sfml-template
    PUBLIC
    ${CMAKE_SOURCE_DIR}/external/skia/out/Static/libskia.a
)

if(${APPLE})
    target_link_libraries(
        skia-sfml-template
        PUBLIC
        "-framework CoreServices"
        "-framework CoreFoundation"
        "-framework CoreGraphics"
        "-framework CoreText"
    )
endif()
