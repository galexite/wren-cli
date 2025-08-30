cmake_minimum_required(VERSION 3.30)

project(wren_cli VERSION 0.4.0 LANGUAGES C)

include(GNUInstallDirs)

set(CMAKE_C_STANDARD 99)

set(wren_SOURCE_DIR "" CACHE PATH "If set to non-empty path, import this checkout of wren as a subdirectory, instead of using find_package")

add_subdirectory("src")
# add_subdirectory("test")
