cmake_minimum_required(VERSION 3.14)

# Hardcoding the compiler and arch since all our projects currently use the same one
# Add new targets to this file if other compiler/arch combinations need to be supported
set(FREERTOS_COMPILER_GCC GCC)
set(FREERTOS_ARCH_ARM_CM4F ARM_CM4F)

add_library(freertos_gcc_armcm4f
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

target_include_directories(freertos_gcc_armcm4f
    PUBLIC
    include
    portable/${FREERTOS_COMPILER_GCC}/${FREERTOS_ARCH_ARM_CM4F}
    ${FREERTOS_CONFIG_FOLDER}
)