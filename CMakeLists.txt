cmake_minimum_required(VERSION 2.8.6)

project(entwine)

set(CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} -std=c++11 -O3 -Wno-deprecated-declarations -Wall -Werror -pedantic -fexceptions -frtti -g"
)

set(BASE "${CMAKE_CURRENT_SOURCE_DIR}")

include_directories(
    "${BASE}"
    "${BASE}/third/"
)

set(SOURCES
    "${BASE}/compression/stream.cpp"
    "${BASE}/compression/util.cpp"
    "${BASE}/http/collector.cpp"
    "${BASE}/http/curl.cpp"
    "${BASE}/http/s3.cpp"
    "${BASE}/third/jsoncpp.cpp"
    "${BASE}/tree/multi-batcher.cpp"
    "${BASE}/tree/point-info.cpp"
    "${BASE}/tree/registry.cpp"
    "${BASE}/tree/roller.cpp"
    "${BASE}/tree/sleepy-tree.cpp"
    "${BASE}/types/bbox.cpp"
    "${BASE}/types/dim-info.cpp"
    "${BASE}/types/schema.cpp"
)

set(ENTWINE_SRC ${SOURCES} "${BASE}/kernel/entwine.cpp")
set(REPROJ_SRC  ${SOURCES} "${BASE}/kernel/post-reproject.cpp")

add_executable(entwine ${ENTWINE_SRC})
add_executable(reproj  ${REPROJ_SRC})

target_link_libraries(entwine pdalcpp curl crypto)
target_link_libraries(reproj  pdalcpp pdal_util curl crypto)
