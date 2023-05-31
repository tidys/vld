cmake_minimum_required(VERSION 3.0.0)
set(app "vld")
project(${app} VERSION 2.5.1)

set(vld_src
    ${CMAKE_CURRENT_LIST_DIR}/src/callstack.h
    ${CMAKE_CURRENT_LIST_DIR}/src/criticalsection.h
    ${CMAKE_CURRENT_LIST_DIR}/src/crtmfcpatch.h
    ${CMAKE_CURRENT_LIST_DIR}/src/dbghelp.h
    ${CMAKE_CURRENT_LIST_DIR}/src/map.h
    ${CMAKE_CURRENT_LIST_DIR}/src/ntapi.h
    ${CMAKE_CURRENT_LIST_DIR}/src/ntapi.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/resource.h
    ${CMAKE_CURRENT_LIST_DIR}/src/set.h
    ${CMAKE_CURRENT_LIST_DIR}/src/stdafx.h
    ${CMAKE_CURRENT_LIST_DIR}/src/stdafx.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/tree.h
    ${CMAKE_CURRENT_LIST_DIR}/src/utility.h
    ${CMAKE_CURRENT_LIST_DIR}/src/utility.cpp
    ${CMAKE_CURRENT_LIST_DIR}/setup/version.h
    ${CMAKE_CURRENT_LIST_DIR}/src/vld.h
    ${CMAKE_CURRENT_LIST_DIR}/src/vld_def.h
    ${CMAKE_CURRENT_LIST_DIR}/src/vldallocator.h
    ${CMAKE_CURRENT_LIST_DIR}/src/vldheap.h
    ${CMAKE_CURRENT_LIST_DIR}/src/vldint.h

    ${CMAKE_CURRENT_LIST_DIR}/src/callstack.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/dllspatches.cpp

    ${CMAKE_CURRENT_LIST_DIR}/src/vld.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/vldapi.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/vldheap.cpp
    ${CMAKE_CURRENT_LIST_DIR}/src/vld_hooks.cpp
)

if(MSVC)
    add_definitions("-DUNICODE" "-D_UNICODE")
    add_definitions("-D_WIN32_WINNT=0x0502")
    add_definitions("-DWIN32")
    set(CMAKE_GENERATOR_VISUAL_STUDIO_VERSION 14)
endif(MSVC)

include(./lib/cppformat/CMakeLists.txt)

add_library(${app} SHARED ${vld_src})
message(${cppformat})
target_link_libraries(${app} PUBLIC ${cppformat})
target_include_directories(${app} PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/lib
    ${CMAKE_CURRENT_LIST_DIR}/lib/dbghelp/include
    ${CMAKE_CURRENT_LIST_DIR}/setup
)
source_group(TREE ${CMAKE_CURRENT_LIST_DIR} FILES ${vld_src})