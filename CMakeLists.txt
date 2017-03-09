# cmake -DCMAKE_TOOLCHAIN_FILE=~/bfprefix/cmake/CMakeToolchain_VMM.txt ..

cmake_minimum_required(VERSION 3.4)
project(bfunwind C CXX)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    set(CMAKE_INSTALL_PREFIX "$ENV{HOME}/bfprefix" CACHE PATH "default bareflank prefix" FORCE)
endif()

include("${CMAKE_INSTALL_PREFIX}/cmake/CMakeGlobal_Project.txt")

# ------------------------------------------------------------------------------
# Subdirectories
# ------------------------------------------------------------------------------

add_subdirectory(src)

# ------------------------------------------------------------------------------
# Install
# ------------------------------------------------------------------------------

install(FILES include/ia64_cxx_abi.h DESTINATION ${BAREFLANK_SYSROOT_PATH}/include RENAME unwind.h)
