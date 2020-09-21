cmake_minimum_required(VERSION 3.16)
project(cmake_cjpeg_djpeg C)

set(CMAKE_C_STANDARD 99)

include(${jpeg_PREFIX}/lib/jpeg/jpeg.cmake)

add_executable(cjpeg cjpeg.c cdjpeg)
add_executable(djpeg djpeg.c cdjpeg)
target_include_directories(cjpeg PUBLIC ${jpeg_INCLUDE_DIRS})
target_include_directories(djpeg PUBLIC ${jpeg_INCLUDE_DIRS})
target_link_libraries(cjpeg jpeg)
target_link_libraries(djpeg jpeg)
