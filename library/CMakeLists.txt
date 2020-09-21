cmake_minimum_required(VERSION 3.16)
project(cmake_jpeg C)

set(CMAKE_C_STANDARD 99)

file(GLOB jpeg_LIBRARY_SOURCES RELATIVE ${CMAKE_SOURCE_DIR} "*.c")
file(GLOB jpeg_LIBRARY_HEADERS RELATIVE ${CMAKE_SOURCE_DIR} "*.h")

if(MSVC)
	set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
endif()

add_library(jpeg SHARED ${jpeg_LIBRARY_SOURCES} ${jpeg_LIBRARY_HEADERS})
add_library(jpeg_static STATIC ${jpeg_LIBRARY_SOURCES} ${jpeg_LIBRARY_HEADERS})

SET(jpeg_INCLUDE_PATH "include")

target_include_directories(jpeg PUBLIC
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
  "$<INSTALL_INTERFACE:$<INSTALL_PREFIX>/${jpeg_INCLUDE_PATH}>")

target_include_directories(jpeg_static PUBLIC
  "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
  "$<INSTALL_INTERFACE:$<INSTALL_PREFIX>/${jpeg_INCLUDE_PATH}>")

install(TARGETS jpeg DESTINATION lib EXPORT jpeg)
install(TARGETS jpeg_static DESTINATION lib EXPORT jpeg_static)
install(FILES ${jpeg_LIBRARY_HEADERS} DESTINATION ${jpeg_INCLUDE_PATH})
install(EXPORT jpeg DESTINATION lib/jpeg)
install(EXPORT jpeg_static DESTINATION lib/jpeg_static)
