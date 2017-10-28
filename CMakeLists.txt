cmake_minimum_required(VERSION 3.5.1)
project (fancyblink C)

include(ExternalProject) 
ExternalProject_Add(libopencm3
    GIT_REPOSITORY https://github.com/libopencm3/libopencm3.git
    SOURCE_DIR "${CMAKE_SOURCE_DIR}/libopencm3"
    CONFIGURE_COMMAND ""
    UPDATE_COMMAND ""
    PATCH_COMMAND ""
    BUILD_COMMAND make
    BUILD_IN_SOURCE 1
    TEST_COMMAND ""
    INSTALL_COMMAND ""
)

include_directories("${CMAKE_SOURCE_DIR}/libopencm3/include")
link_directories("${CMAKE_SOURCE_DIR}/libopencm3/lib")

add_definitions(-DSTM32F4)

set(STM32F4_FLAGS "-mthumb -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=fpv4-sp-d16")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -ggdb3 -O0 -Wall --std=gnu99 -fno-common ${STM32F4_FLAGS}")
set(CMAKE_EXE_LINKER_FLAGS "-T ${CMAKE_SOURCE_DIR}/stm32f4-discovery.ld --specs=nosys.specs -Wl,--gc-sections -nostartfiles")

set(SOURCES fancyblink.c)

add_executable (fancyblink ${SOURCES})
add_dependencies(fancyblink libopencm3)
target_link_libraries(fancyblink opencm3_stm32f4)

