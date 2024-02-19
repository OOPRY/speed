cmake_minimum_required(VERSION 3.5)

# Project name and version
project(libspeex VERSION 1.2.0)

# Specify the C standard
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED True)

# Include directories
include_directories(include)

# Source files
file(GLOB SOURCES "src/*.c")

# Define the library
add_library(speex ${SOURCES})

target_compile_options(speex PRIVATE -D__GNU_LIBRARY__ -Wno-unused-but-set-variable -Wno-deprecated-non-prototype)
target_link_libraries(speex ogg)

# Specify library's public headers
set_target_properties(speex PROPERTIES PUBLIC_HEADER "include/speex/speex.h;include/speex/speex_bits.h")

# Installation setup
install(TARGETS speex
    LIBRARY DESTINATION lib
    PUBLIC_HEADER DESTINATION include/speex
)