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

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/ThirdParty/PSCommon/XnLib/)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/Source/Drivers/OniFile)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/Source/Drivers/PS1080)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/Source/)
