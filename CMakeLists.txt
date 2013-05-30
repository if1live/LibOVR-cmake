cmake_minimum_required(VERSION 2.6)
project( LibOVR )

if(APPLE)
file( GLOB PLATFORM_FILES
	Src/Kernel/OVR_ThreadsPthread.cpp
	Src/OVR_OSX_DeviceManager.cpp
	Src/OVR_OSX_DeviceManager.h
	Src/OVR_OSX_HIDDevice.cpp
	Src/OVR_OSX_HIDDevice.h
	Src/OVR_OSX_HMDDevice.cpp
	Src/OVR_OSX_HMDDevice.h
	Src/OVR_OSX_SensorDevice.cpp )
	
elseif(MSVC)
file( GLOB PLATFORM_FILES
	Src/Kernel/OVR_ThreadsWinAPI.cpp
	Src/OVR_Win32_DeviceManager.cpp
	Src/OVR_Win32_DeviceManager.h
	Src/OVR_Win32_DeviceStatus.cpp
	Src/OVR_Win32_DeviceStatus.h
	Src/OVR_Win32_HIDDevice.cpp
	Src/OVR_Win32_HIDDevice.h
	Src/OVR_Win32_HMDDevice.cpp
	Src/OVR_Win32_HMDDevice.h
	Src/OVR_Win32_SensorDevice.cpp
	Src/OVR_Win32_SensorDevice.h )
	
else()
message( FATAL_ERROR "LibOVR support Win32/MacOS" )
endif()

add_definitions(-DUNICODE -D_UNICODE)

include_directories( Include )

file( GLOB INTERFACE_HEADERS Include/*.h )

file( GLOB LIBOVR_FILES
	Src/Kernel/OVR_Alg.cpp
	Src/Kernel/OVR_Alg.h
	Src/Kernel/OVR_Allocator.cpp
	Src/Kernel/OVR_Allocator.h
	Src/Kernel/OVR_Array.h
	Src/Kernel/OVR_Atomic.cpp
	Src/Kernel/OVR_Atomic.h
	Src/Kernel/OVR_Color.h
	Src/Kernel/OVR_ContainerAllocator.h
	Src/Kernel/OVR_File.cpp
	Src/Kernel/OVR_File.h
	Src/Kernel/OVR_FileFILE.cpp
	Src/Kernel/OVR_Hash.h
	Src/Kernel/OVR_KeyCodes.h
	Src/Kernel/OVR_List.h
	Src/Kernel/OVR_Log.cpp
	Src/Kernel/OVR_Log.h
	Src/Kernel/OVR_Math.cpp
	Src/Kernel/OVR_Math.h
	Src/Kernel/OVR_RefCount.cpp
	Src/Kernel/OVR_RefCount.h
	Src/Kernel/OVR_Std.cpp
	Src/Kernel/OVR_Std.h
	Src/Kernel/OVR_String.cpp
	Src/Kernel/OVR_String.h
	Src/Kernel/OVR_String_FormatUtil.cpp
	Src/Kernel/OVR_String_PathUtil.cpp
	Src/Kernel/OVR_StringHash.h
	Src/Kernel/OVR_SysFile.cpp
	Src/Kernel/OVR_SysFile.h
	Src/Kernel/OVR_System.cpp
	Src/Kernel/OVR_System.h
	Src/Kernel/OVR_Threads.h
	Src/Kernel/OVR_Timer.cpp
	Src/Kernel/OVR_Timer.h
	Src/Kernel/OVR_Types.h
	Src/Kernel/OVR_UTF8Util.cpp
	Src/Kernel/OVR_UTF8Util.h
	Src/OVR_Device.h
	Src/OVR_DeviceConstants.h
	Src/OVR_DeviceHandle.cpp
	Src/OVR_DeviceHandle.h
	Src/OVR_DeviceImpl.cpp
	Src/OVR_DeviceImpl.h
	Src/OVR_DeviceMessages.h
	Src/OVR_HIDDevice.h
	Src/OVR_HIDDeviceBase.h
	Src/OVR_HIDDeviceImpl.h
	Src/OVR_LatencyTestImpl.cpp
	Src/OVR_LatencyTestImpl.h
	Src/OVR_SensorFilter.cpp
	Src/OVR_SensorFilter.h
	Src/OVR_SensorFusion.cpp
	Src/OVR_SensorFusion.h
	Src/OVR_SensorImpl.cpp
	Src/OVR_SensorImpl.h
	Src/OVR_ThreadCommandQueue.cpp
	Src/OVR_ThreadCommandQueue.h
	Src/Util/Util_LatencyTest.cpp
	Src/Util/Util_LatencyTest.h
	Src/Util/Util_MagCalibration.cpp
	Src/Util/Util_MagCalibration.h
	Src/Util/Util_Render_Stereo.cpp
	Src/Util/Util_Render_Stereo.h )

source_group( include FILES ${INTERFACE_HEADERS} )
source_group( src FILES ${LIBOVR_FILES} )
source_group( platform FILES ${PLATFORM_FILES} )

add_library( LibOVR STATIC 
	${LIBOVR_FILES} 
	${PLATFORM_FILES} )