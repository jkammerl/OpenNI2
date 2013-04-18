cmake_minimum_required(VERSION 2.8)

project(OpenNI2)

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/modules/" ${CMAKE_MODULE_PATH})

find_package(libjpeg REQUIRED )
find_package(libusb-1.0 REQUIRED)

if(UNIX AND M64)
    add_compile_flags("-fPIC")
endif()

# These definitions are meant for the third-party GL stuff.
if(WIN32)
    add_definitions(-DWIN32)
endif()
if(APPLE)
    add_definitions(-DMACOS)
endif()
if(UNIX)
    add_definitions(-DUNIX)
endif()

add_definitions(${LIBUSB_1_DEFINITIONS} -DOPENNI2_EXPORT)

include_directories(${LIBJPEG_INCLUDE_DIR} 
                    ${LIBUSB_1_INCLUDE_DIRS}
                    )

set(EXPORT_INCLUDES ${CMAKE_CURRENT_LIST_DIR}/Include)

set(GLOBAL_INCLUDES ${EXPORT_INCLUDES})

set (PLUGIN_DIR bin/OpenNI2/Drivers)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/ThirdParty/PSCommon/XnLib/)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/Source/Drivers/OniFile)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/Source/Drivers/PS1080)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/Source/)


install(FILES ${CMAKE_CURRENT_LIST_DIR}/Config/OpenNI2.pc DESTINATION lib/pkgconfig/)

install(FILES ${CMAKE_CURRENT_LIST_DIR}/Config/PS1080.ini DESTINATION /etc/OpenNI2/)
install(FILES ${CMAKE_CURRENT_LIST_DIR}/Config/OpenNI.ini DESTINATION /etc/OpenNI2/)

install(FILES ${CMAKE_CURRENT_LIST_DIR}/Config/55-primesense-usb.rules DESTINATION /etc/udev/rules.d/)
install(FILES ${CMAKE_CURRENT_LIST_DIR}/Config/blacklist-psengine.conf DESTINATION /etc/modprobe.d/)

install(EXPORT OpenNI2-exports DESTINATION share/OpenNI2)

SET(CPACK_GENERATOR "DEB")
SET(CPACK_PACKAGE_DESCRIPTION_SUMMARY "OpenNI2 framework")
SET(CPACK_DEBIAN_PACKAGE_MAINTAINER "Julius Kammerl (jkammerl@willowgarage.com)") #required

SET(CPACK_PACKAGE_VENDOR "Willow Garage")
SET(CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_CURRENT_SOURCE_DIR}/README")
SET(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/LICENSE")
SET(CPACK_PACKAGE_VERSION_MAJOR "2")
SET(CPACK_PACKAGE_VERSION_MINOR "0")
SET(CPACK_PACKAGE_VERSION_PATCH "0")

SET(CPACK_PACKAGING_INSTALL_PREFIX ${CMAKE_INSTALL_PREFIX})

INCLUDE(CPack)