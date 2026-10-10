# Standalone build of the tools Darling needs (ld64, ar, ranlib, lipo), e.g. for distribution packages.
# Darling itself adds the subdirectories below directly and does not use this file.
cmake_minimum_required(VERSION 3.18)
project(darling-cctools C CXX)

set(APPLE_TARGET_TRIPLET_PRIMARY "x86_64-apple-darwin20" CACHE STRING "Target triple the tools are named after")
set(TARGET_x86_64 ON)
# Darling defines this globally; it enables Darling-specific fixes in these tools
add_compile_definitions(DARLING)

add_subdirectory(cctools/ld64/src)
add_subdirectory(cctools/ar)
add_subdirectory(cctools/misc)

include(GNUInstallDirs)
install(TARGETS ${APPLE_TARGET_TRIPLET_PRIMARY}-ld ${APPLE_TARGET_TRIPLET_PRIMARY}-ar ranlib lipo
	RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}")
install(DIRECTORY cctools/include/ DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/darling-cctools")
