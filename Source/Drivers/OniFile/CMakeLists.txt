
#### OniFile Device

include_directories(
    ${CMAKE_CURRENT_LIST_DIR}/Formats/
    ${GLOBAL_INCLUDES}
)

set(GLOBAL_INCLUDES ${GLOBAL_INCLUDES} ${CMAKE_CURRENT_LIST_DIR}/Include ${CMAKE_CURRENT_LIST_DIR}/Formats PARENT_SCOPE)

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

set(OPENNI2_PLUGINS ${OPENNI2_PLUGINS} OniFileLib PARENT_SCOPE)

if(MACOSX)
    set_property(TARGET OniFileLib PROPERTY SUFFIX .dylib)
endif()

install(TARGETS OniFileLib DESTINATION bin/OpenNI2/Drivers)