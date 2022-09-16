cmake_minimum_required(VERSION 3.14)

# Set the target name based on the name of the binary directory. This allows for the HAL to 
# be build with different configurations when included by different projects. 
get_filename_component(TARGET_NAME ${CMAKE_CURRENT_BINARY_DIR} NAME)

# Hardcoding the compiler and arch since all our projects currently use the same one
# Add new targets to this file if other compiler/arch combinations need to be supported
set(FREERTOS_COMPILER_GCC GCC)
set(FREERTOS_ARCH_ARM_CM4F ARM_CM4F)

add_library(${TARGET_NAME}
    STATIC
    croutine.c
    event_groups.c
    list.c
    queue.c
    stream_buffer.c
    tasks.c
    timers.c
    portable/${FREERTOS_COMPILER_GCC}/${FREERTOS_ARCH_ARM_CM4F}/port.c
)

if (NOT EXISTS ${FREERTOS_CONFIG_FOLDER}/FreeRTOSConfig.h)
    message(FATAL_ERROR "Make sure FreeRTOSConfig.h exists in FREERTOS_CONFIG_FOLDER(${FREERTOS_CONFIG_FOLDER})")
endif()

target_include_directories(${TARGET_NAME}
    PUBLIC
    include
    portable/${FREERTOS_COMPILER_GCC}/${FREERTOS_ARCH_ARM_CM4F}
    ${FREERTOS_CONFIG_FOLDER}
)