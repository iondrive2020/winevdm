file(GLOB SOURCE *.c *.cpp *.rc)
add_library(msacm SHARED ${SOURCE} ${CMAKE_CURRENT_BINARY_DIR}/msacm.def msacm.dll16.obj)
include_directories(../wine)
add_definitions(-D_X86_ -D__WINESRC__ -D__i386__ -DHAVE_STRNCASECMP -DHAVE__STRNICMP -D_WINTERNL_ -DNtCurrentTeb=NtCurrentTeb__ -DDECLSPEC_HIDDEN= -Dstrncasecmp=_strnicmp)
spec_build(msacm.dll16 msacm)
target_link_libraries(msacm libwine winecrt0 krnl386 msacm32.lib)
set_target_properties(msacm PROPERTIES SUFFIX ".dll16")
