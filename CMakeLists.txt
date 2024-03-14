cmake_minimum_required(VERSION 3.5)

# Project name and version
project(libspeex VERSION 1.2.0)

# Specify the C standard
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED True)

# Source files
file(GLOB SOURCES "src/*.c")

file(GLOB LIB_SOURCES "libspeex/*.c")

# Define the library
add_library(speex ${SOURCES} ${LIB_SOURCES})

target_compile_options(speex PRIVATE -D__GNU_LIBRARY__ -DFLOATING_POINT -DUSE_SMALLFT -DEXPORT= -Wno-unused-but-set-variable -Wno-deprecated-non-prototype)
target_link_libraries(speex PUBLIC ogg)
target_include_directories(speex PUBLIC "include")

# Specify library's public headers
set_target_properties(speex PROPERTIES PUBLIC_HEADER "include/speex/speex.h;include/speex/speex_bits.h")

# Installation setup
install(TARGETS speex
    LIBRARY DESTINATION lib
    PUBLIC_HEADER DESTINATION include/speex
)