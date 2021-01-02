cmake_minimum_required(VERSION 3.10 FATAL_ERROR)
project(ae-template LANGUAGES CXX VERSION 0.0.0)

# detect operating system and host processor
message(STATUS "We are on a ${CMAKE_SYSTEM_NAME} system")
message(STATUS "The host processor is ${CMAKE_HOST_SYSTEM_PROCESSOR}")

# c++ flags
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_definitions(-D_UNICODE -DUNICODE)

# cmake helpers
if(WIN32)
	# Create a regular windowed application instead of the default console subsystem target
	set(AE_EXE_TYPE WIN32)
	# Use main instead of WinMain
	set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /ENTRY:mainCRTStartup")
endif()

set(AE_LEAN_AND_MEAN ON CACHE BOOL "Only build ae library. Examples and tests will be disabled.")
add_subdirectory(deps/aether-game-utils)

add_executable(game ${AE_EXE_TYPE} src/main.cpp)
target_link_libraries(game ae)
