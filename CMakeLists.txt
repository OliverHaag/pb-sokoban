project(pb-sokoban)
cmake_minimum_required(VERSION 2.6.0)

set(TOOLCHAIN_PATH ${CMAKE_FIND_ROOT_PATH}/../..)

find_package(Freetype REQUIRED)

add_custom_command(
	OUTPUT ${CMAKE_SOURCE_DIR}/images/images.c
	COMMAND ${TOOLCHAIN_PATH}/bin/pbres -c ${CMAKE_SOURCE_DIR}/images/images.c -4 ${CMAKE_SOURCE_DIR}/images/*.bmp)

add_executable(pb-sokoban.app
	${CMAKE_SOURCE_DIR}/src/sokoban.c
	${CMAKE_SOURCE_DIR}/images/images.c)

include_directories(${CMAKE_SOURCE_DIR}/src ${FREETYPE_INCLUDE_DIRS})
target_link_libraries(pb-sokoban.app pthread inkview freetype)

install(TARGETS pb-sokoban.app DESTINATION bin)
