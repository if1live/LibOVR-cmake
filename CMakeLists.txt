cmake_minimum_required(VERSION 2.6)
project( LibOVR )

if(APPLE)
	file( GLOB PLATFORM_FILES
		"Src/Kernel/OVR_ThreadsPthread.*"
		"Src/OVR_OSX_*.*" )
	
elseif(WIN32)
	add_definitions(-DMINGW_HAS_SECURE_API)
	file( GLOB PLATFORM_FILES
		"Src/Kernel/OVR_ThreadsWinAPI.*"
		"Src/OVR_Win32_*.*" )

else()
	# Linux
	file( GLOB PLATFORM_FILES 
		"Src/Kernel/OVR_ThreadsPthread.*"
		"Src/OVR_Linux_*.*" )
	
endif()

add_definitions(-DUNICODE -D_UNICODE)
set( LIBOVR_INC_DIR 
	"${CMAKE_CURRENT_SOURCE_DIR}/Src"
	"${CMAKE_CURRENT_SOURCE_DIR}/Include" )

include_directories( Include Src )

file( GLOB INTERFACE_HEADERS Include/*.h )

file( GLOB LIBOVR_FILES
	"Src/Kernel/OVR_Alg.*"
	"Src/Kernel/OVR_Allocator.*"
	"Src/Kernel/OVR_Array.*"
	"Src/Kernel/OVR_Atomic.*"
	"Src/Kernel/OVR_Color.*"
	"Src/Kernel/OVR_ContainerAllocator.*"
	"Src/Kernel/OVR_File.*"
	"Src/Kernel/OVR_FileFILE.*"
	"Src/Kernel/OVR_Hash.*"
	"Src/Kernel/OVR_KeyCodes.*"
	"Src/Kernel/OVR_List.*"
	"Src/Kernel/OVR_Log.*"
	"Src/Kernel/OVR_Math.*"
	"Src/Kernel/OVR_RefCount.*"
	"Src/Kernel/OVR_Std.*"
	"Src/Kernel/OVR_String.*"
	"Src/Kernel/OVR_String_FormatUtil.*"
	"Src/Kernel/OVR_String_PathUtil.*"
	"Src/Kernel/OVR_StringHash.*"
	"Src/Kernel/OVR_SysFile.*"
	"Src/Kernel/OVR_System.*"
	"Src/Kernel/OVR_Threads.*"
	"Src/Kernel/OVR_Timer.*"
	"Src/Kernel/OVR_Types.*"
	"Src/Kernel/OVR_UTF8Util.*"
	"Src/OVR_Device.*"
	"Src/OVR_DeviceConstants.*"
	"Src/OVR_DeviceHandle.*"
	"Src/OVR_DeviceImpl.*"
	"Src/OVR_DeviceMessages.*"
	"Src/OVR_HIDDevice.*"
	"Src/OVR_HIDDeviceBase.*"
	"Src/OVR_HIDDeviceImpl.*"
	"Src/OVR_LatencyTestImpl.*"
	"Src/OVR_SensorFilter.*"
	"Src/OVR_SensorFusion.*"
	"Src/OVR_SensorImpl.*"
	"Src/OVR_ThreadCommandQueue.*"
	"Src/OVR_JSON.*"
	"Src/OVR_Profile.*"
	"Src/Util/Util_LatencyTest.*"
	"Src/Util/Util_MagCalibration.*"
	"Src/Util/Util_Render_Stereo.*" )

source_group( include FILES ${INTERFACE_HEADERS} )
source_group( src FILES ${LIBOVR_FILES} )
source_group( platform FILES ${PLATFORM_FILES} )

add_library( LibOVR STATIC 
	${LIBOVR_FILES} 
	${PLATFORM_FILES} )
set_target_properties(LibOVR PROPERTIES PREFIX "")

if( NOT (CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR) )
	set( LIBOVR_INC_DIR 
		"${CMAKE_CURRENT_SOURCE_DIR}/Include" 
		"${CMAKE_CURRENT_SOURCE_DIR}/Src"
		PARENT_SCOPE )
endif()
