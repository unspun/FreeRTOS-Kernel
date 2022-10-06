cmake_minimum_required(VERSION 3.14)

set(freertos_internal_dir ${CMAKE_CURRENT_LIST_DIR} CACHE INTERNAL "")

function(validate_freertos_config freertos_config_folder)
    if (NOT EXISTS ${freertos_config_folder}/FreeRTOSConfig.h)
        message(FATAL_ERROR "Make sure FreeRTOSConfig.h exists in freertos_config_folder(${freertos_config_folder})")
    endif()
endfunction()

function(unspun_add_freertos target_name freertos_config_folder)

    validate_freertos_config(${freertos_config_folder})
    
    # Hardcoding the compiler and arch since all our projects currently use the same one
    # Add new targets to this file if other compiler/arch combinations need to be supported
    set(FREERTOS_COMPILER_GCC GCC)
    set(FREERTOS_ARCH_ARM_CM4F ARM_CM4F)

    add_library(${target_name}
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

    target_include_directories(${target_name}
        PUBLIC
        include
        portable/${FREERTOS_COMPILER_GCC}/${FREERTOS_ARCH_ARM_CM4F}
        ${freertos_config_folder}
    )

endfunction()