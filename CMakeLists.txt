# Bare cmake

cmake_minimum_required(VERSION 2.6)

set(KEYWORD "installation-guides")

# Start a project.
project(${KEYWORD})

find_package(YARP REQUIRED)
list(APPEND CMAKE_MODULE_PATH ${YARP_MODULE_PATH})
include(YarpInstallationHelpers)
yarp_configure_external_installation(roboticslab-installation-guides)

file(GLOB md ${CMAKE_CURRENT_SOURCE_DIR}/*.md)
yarp_install(FILES ${md} DESTINATION ${ROBOTICSLAB-INSTALLATION-GUIDES_CONTEXTS_INSTALL_DIR})

# uninstall target
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/template/ROBOTICSLAB_INSTALLATION_GUIDESConfigUninstall.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/ROBOTICSLAB_INSTALLATION_GUIDESConfigUninstall.cmake" IMMEDIATE @ONLY)

add_custom_target(uninstall
    COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/ROBOTICSLAB_INSTALLATION_GUIDESConfigUninstall.cmake)

