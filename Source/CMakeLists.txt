
include_directories(${GLOBAL_INCLUDES})

set(OpenNI2_SRC
    Core/OniContext.cpp
    Core/OniDataRecords.cpp
    Core/OniDevice.cpp
    Core/OniDeviceDriver.cpp
    Core/OniDriverHandler.cpp
    Core/OniRecorder.cpp
    Core/OniStream.cpp
    Core/OniStreamFrameHolder.cpp
    Core/OniSyncedStreamsFrameHolder.cpp
    Core/OpenNI.cpp

    Drivers/OniFile/Formats/XnStreamCompression.cpp
)

add_library(OpenNI2 SHARED ${OpenNI2_SRC})
target_link_libraries(OpenNI2 XnLib ${LIBJPEG_LIBRARY})

if(UNIX)
    set_property(TARGET OpenNI2 PROPERTY COMPILE_FLAGS "-fvisibility=hidden")
endif()

set_property(TARGET OpenNI2 PROPERTY LINK_INTERFACE_LIBRARIES "")

install(DIRECTORY ${EXPORT_INCLUDES}/ DESTINATION include/OpenNI2)
install(TARGETS OpenNI2 EXPORT OpenNI2-exports
    RUNTIME DESTINATION bin
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)
