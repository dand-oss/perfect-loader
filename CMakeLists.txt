cmake_minimum_required(VERSION 3.30)
project(perfect-loader
    VERSION "1.0"
    DESCRIPTION "A perfect loader implementation"
    HOMEPAGE_URL "https://github.com/EvanMcBroom/perfect-loader"
    LANGUAGES C CXX
)
if (${CMAKE_PROJECT_NAME} STREQUAL ${PROJECT_NAME})
    set(MAIN_PROJECT TRUE)
    set(CLIB pl)
else()
    set(MAIN_PROJECT FALSE)
    set(PROJECT_NAME "library_pl++")
    set(CLIB library_pl)
endif()

###############
# ASI default settings
list(APPEND CMAKE_MODULE_PATH "$ENV{ASV_CMAKE}")
include(asv_cmake_defaults)
asv_cmake_defaults( )
###############

install(
    FILES include/perfect_loader.hpp include/perfect_loader.h
    DESTINATION include/perfect_loader
    )

install(
    DIRECTORY include/pl
    DESTINATION include/perfect_loader
    )

add_subdirectory(source)
