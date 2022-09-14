cmake_minimum_required(VERSION 3.14)

project(cmake_build)

set(FREERTOS_CONFIG_FOLDER ${CMAKE_CURRENT_SOURCE_DIR})

add_subdirectory(../ freertos)