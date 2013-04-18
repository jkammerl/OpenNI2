 if(WIN32)
	 set(XnLib_SRC 
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnUSBWin32.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32CriticalSection.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Debug.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Events.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Files.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32INI.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Keyboard.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Memory.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Mutex.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Network.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32OS.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Processes.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Semaphore.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32SharedLibrary.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32SharedMemory.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Strings.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Threads.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Win32/XnWin32Time.cpp
	)
endif()

if(UNIX)
    set (PLUGIN_DIR_TEMPLATE  ${CMAKE_INSTALL_PREFIX}/${PLUGIN_DIR})
    configure_file(${CMAKE_CURRENT_LIST_DIR}/Include/Linux-x86/XnOSLinux-x86.h.in
                   ${CMAKE_CURRENT_LIST_DIR}/Include/Linux-x86/XnOSLinux-x86.h
                   @ONLY)

	set(XnLib_SRC
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxCriticalSections.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxDebug.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxEvents.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxFiles.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxINI.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxKeyboard.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxMemory.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxMutex.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxNetwork.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxPosixEvents.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxPosixNamedEvents.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxProcesses.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxSharedLibs.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxSharedMemory.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxStrings.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxSysVNamedEvents.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxThreads.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxTime.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxUSB.cpp
	    ${CMAKE_CURRENT_LIST_DIR}/Source/Linux/XnLinuxUSBDevice.cpp
	)
endif()

set(XnLib_SRC ${XnLib_SRC}
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnDump.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnDumpFileWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnErrorLogger.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnFiles.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnFPSCalculator.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnLib.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnLog.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnLogAndroidWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnLogConsoleWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnLogFileWriter.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnOS.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnOSMemoryProfiling.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnProfiling.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnScheduler.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnStatus.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnStrings.cpp
#    ${CMAKE_CURRENT_LIST_DIR}/Source/XnSytmmetricMatrix3x3.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnThreads.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnUSB.cpp
    ${CMAKE_CURRENT_LIST_DIR}/Source/XnVector3D.cpp
)

set (XnLib_INCLUDE_DIR ${CMAKE_CURRENT_LIST_DIR}/Include) 

if(WINDOWS)
    set(XnLib_INCLUDE_DIR ${XnLib_INCLUDE_DIR} ${CMAKE_CURRENT_LIST_DIR}/Driver/Win32/Build/sys)
endif()

include_directories(${XnLib_INCLUDE_DIR})

add_library(XnLib SHARED ${XnLib_SRC})
target_link_libraries(XnLib ${LIBUSB_1_LIBRARIES})

set(GLOBAL_INCLUDES ${GLOBAL_INCLUDES} ${XnLib_INCLUDE_DIR} PARENT_SCOPE)

install(TARGETS XnLib EXPORT OpenNI2-exports
    RUNTIME DESTINATION bin
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

