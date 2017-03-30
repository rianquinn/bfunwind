# ------------------------------------------------------------------------------
# CMake Includes
# ------------------------------------------------------------------------------

include("${CMAKE_INSTALL_PREFIX}/cmake/CMakeGlobal_Includes.txt")

# ------------------------------------------------------------------------------
# Exports
# ------------------------------------------------------------------------------

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DCOMPILING_UNWIND")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DCOMPILING_UNWIND")

# ------------------------------------------------------------------------------
# Custom Flags
# ------------------------------------------------------------------------------

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-rtti")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-exceptions")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-threadsafe-statics")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-stack-protector")

# ------------------------------------------------------------------------------
# Targets
# ------------------------------------------------------------------------------

list(APPEND SOURCES
    dwarf4.cpp
    eh_frame.cpp
    ia64_cxx_abi.cpp
    registers_intel_x64.asm
)

add_library(unwind OBJECT ${SOURCES})
add_library(bfunwind SHARED $<TARGET_OBJECTS:unwind>)
add_library(bfunwind_static STATIC $<TARGET_OBJECTS:unwind>)

# ------------------------------------------------------------------------------
# Install
# ------------------------------------------------------------------------------

install(TARGETS bfunwind DESTINATION ${BAREFLANK_SYSROOT_PATH}/lib)
install(TARGETS bfunwind_static DESTINATION ${BAREFLANK_SYSROOT_PATH}/lib)
