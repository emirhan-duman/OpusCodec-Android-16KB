cmake_minimum_required(VERSION 3.22.1)

# 16KB Page Size (Google Play 2025 requirement)
set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -Wl,-z,max-page-size=16384")

project(opuscodec)

# Include OPUS (from cloned repo)
set(OPUS_BUILD_TESTING OFF CACHE BOOL "" FORCE)
add_subdirectory(opus)

add_library(easyopus SHARED
        easyopus.cpp
        CodecOpus.cpp
        SamplesConverter.cpp
)

target_include_directories(easyopus PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/codec
        ${CMAKE_CURRENT_SOURCE_DIR}/utils
        ${CMAKE_CURRENT_SOURCE_DIR}/opus/include
)

find_library(log-lib log)

target_link_libraries(
        easyopus
        opus
        ${log-lib}
)
