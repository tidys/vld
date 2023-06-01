set(vld "vld")
set(vld_src
    ${CMAKE_CURRENT_LIST_DIR}/callstack.h
    ${CMAKE_CURRENT_LIST_DIR}/criticalsection.h
    ${CMAKE_CURRENT_LIST_DIR}/crtmfcpatch.h
    ${CMAKE_CURRENT_LIST_DIR}/../lib/dbghelp/include/DbgHelp.h
    ${CMAKE_CURRENT_LIST_DIR}/dbghelp.h
    ${CMAKE_CURRENT_LIST_DIR}/map.h
    ${CMAKE_CURRENT_LIST_DIR}/ntapi.h
    ${CMAKE_CURRENT_LIST_DIR}/ntapi.cpp
    ${CMAKE_CURRENT_LIST_DIR}/resource.h
    ${CMAKE_CURRENT_LIST_DIR}/set.h
    ${CMAKE_CURRENT_LIST_DIR}/stdafx.h
    ${CMAKE_CURRENT_LIST_DIR}/stdafx.cpp
    ${CMAKE_CURRENT_LIST_DIR}/tree.h
    ${CMAKE_CURRENT_LIST_DIR}/utility.h
    ${CMAKE_CURRENT_LIST_DIR}/utility.cpp
    ${CMAKE_CURRENT_LIST_DIR}/../setup/version.h
    ${CMAKE_CURRENT_LIST_DIR}/vld.h
    ${CMAKE_CURRENT_LIST_DIR}/vld_def.h
    ${CMAKE_CURRENT_LIST_DIR}/vldallocator.h
    ${CMAKE_CURRENT_LIST_DIR}/vldheap.h
    ${CMAKE_CURRENT_LIST_DIR}/vldint.h

    ${CMAKE_CURRENT_LIST_DIR}/callstack.cpp
    ${CMAKE_CURRENT_LIST_DIR}/dllspatches.cpp

    ${CMAKE_CURRENT_LIST_DIR}/vld.cpp
    ${CMAKE_CURRENT_LIST_DIR}/vldapi.cpp
    ${CMAKE_CURRENT_LIST_DIR}/vldheap.cpp
    ${CMAKE_CURRENT_LIST_DIR}/vld_hooks.cpp
)

if(MSVC)
    add_definitions("-DUNICODE" "-D_UNICODE")
    add_definitions("-D_WIN32_WINNT=0x0502")
    add_definitions("-DWIN32")
    set(CMAKE_GENERATOR_VISUAL_STUDIO_VERSION 14)
endif(MSVC)

include(${CMAKE_CURRENT_LIST_DIR}/../lib/cppformat/CMakeLists.txt)
add_library(${vld} SHARED ${vld_src})
target_link_libraries(${vld} PRIVATE ${cppformat})
target_link_directories(${vld} PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/../lib/dbghelp/include
)
target_include_directories(${vld} PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/
    ${CMAKE_CURRENT_LIST_DIR}/../lib

    ${CMAKE_CURRENT_LIST_DIR}/../lib/dbghelp/include
    ${CMAKE_CURRENT_LIST_DIR}/../setup
)

# set(CMAKE_GENERATOR_TOOLSET "v120_xp" CACHE STRING "Select platform toolset" FORCE)
# set(CMAKE_GENERATOR_PLATFORM "x86" CACHE STRING "Select target platform" FORCE)
# set(CMAKE_INCLUDE_PATH ${CMAKE_CURRENT_LIST_DIR}/../lib/dbghelp/include ${CMAKE_INCLUDE_PATH})
source_group(TREE ${CMAKE_CURRENT_LIST_DIR}/../ FILES ${vld_src})
