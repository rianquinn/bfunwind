# cmake -DCMAKE_TOOLCHAIN_FILE=~/bfprefix/cmake/CMakeToolchain_VMM_40.txt ..

cmake_minimum_required(VERSION 3.4)
project(bfunwind C CXX)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    if(NOT WIN32 STREQUAL "1")
        set(CMAKE_INSTALL_PREFIX "$ENV{HOME}/bfprefix" CACHE PATH "default install path" FORCE)
    else()
        set(CMAKE_INSTALL_PREFIX "$ENV{HOMEPATH}/bfprefix" CACHE PATH "default install path" FORCE)
    endif()
endif()

include("${CMAKE_INSTALL_PREFIX}/cmake/CMakeGlobal_Project.txt")

# ------------------------------------------------------------------------------
# Flags
# ------------------------------------------------------------------------------

if(CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -nostdlib-c")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -nostdlib-c -nostdinc-c++")
endif()

# ------------------------------------------------------------------------------
# Subdirectories
# ------------------------------------------------------------------------------

add_subdirectory(src)

# ------------------------------------------------------------------------------
# Install
# ------------------------------------------------------------------------------

install(FILES include/ia64_cxx_abi.h DESTINATION ${BAREFLANK_SYSROOT_PATH}/include RENAME unwind.h)
