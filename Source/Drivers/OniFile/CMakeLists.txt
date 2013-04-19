
#### OniFile Device

include_directories(
    ${CMAKE_CURRENT_LIST_DIR}/
    ${EXPORT_INCLUDES}
    ${XnLib_INCLUDE_DIR}
    ${CMAKE_CURRENT_LIST_DIR}/Formats/
)

set(ONI_FORMATS_INCLUDE ${CMAKE_CURRENT_LIST_DIR}/Formats PARENT_SCOPE)

set(OniFile_SRC ${XnLib_SRC}
    ${CMAKE_CURRENT_LIST_DIR}/DataRecords.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Formats/XnCodec.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Formats/XnStreamCompression.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlayerCodecFactory.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlayerDevice.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlayerDriver.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlayerNode.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlayerSource.cpp
    ${CMAKE_CURRENT_LIST_DIR}/PlayerStream.cpp
)

add_library(OniFileLib SHARED ${OniFile_SRC})
target_link_libraries(OniFileLib ${LIBJPEG_LIBRARY})

if(MACOSX)
    set_property(TARGET OniFileLib PROPERTY SUFFIX .dylib)
endif()

install(TARGETS OniFileLib DESTINATION ${PLUGIN_DIR})

set(GLOBAL_INCLUDES ${GLOBAL_INCLUDES} ${CMAKE_CURRENT_LIST_DIR}/Include ${CMAKE_CURRENT_LIST_DIR}/Formats PARENT_SCOPE)