add_compile_options("-DMSDK_REG_SECURE_ADDR(x)=((uint32_t)(x))")

file(GLOB_RECURSE LPC54016_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/CMSIS/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/device/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/device/*.S
    ${CMAKE_CURRENT_SOURCE_DIR}/drivers/*.c
)

add_library(LPC54016-SDK ${LPC54016_SOURCES} STATIC)


target_compile_definitions(LPC54016-SDK PUBLIC
    DEBUG
    CODE_RED
    __NEWLIB__
    CPU_LPC54016JBD100
    CORE_M4
    __FPU_PRESENT=1
    CPP_USE_HEAP
    MTB_BUFFER_SIZE=256
    SERIAL_PORT_TYPE_UART=1
)

target_include_directories(LPC54016-SDK PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/CMSIS
    ${CMAKE_CURRENT_SOURCE_DIR}/device
    ${CMAKE_CURRENT_SOURCE_DIR}/drivers
    ${CMAKE_CURRENT_SOURCE_DIR}/MCUXpresso
)

target_link_libraries(LPC54016-SDK PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/MCUXpresso/libpower_hardabi.a
    ${CMAKE_CURRENT_SOURCE_DIR}/MCUXpresso/libpower_softabi.a
    ${CMAKE_CURRENT_SOURCE_DIR}/MCUXpresso/libfro_calib_hardabi.a
)