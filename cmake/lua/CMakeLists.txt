CMAKE_MINIMUM_REQUIRED(VERSION 3.5)
PROJECT ( lua )

IF( NOT WIN32 )
    message( FATAL_ERROR "Written for window only" )
ENDIF()



# remove warnings
ADD_DEFINITIONS(-D_CRT_SECURE_NO_WARNINGS ) 

SET (HDR_LIBLUA
    ../../3rd/lua/lapi.h 
    ../../3rd/lua/lauxlib.h 
    ../../3rd/lua/lcode.h 
    ../../3rd/lua/lctype.h 
    ../../3rd/lua/ldebug.h 
    ../../3rd/lua/ldo.h 
    ../../3rd/lua/lfunc.h
    ../../3rd/lua/lgc.h 
    ../../3rd/lua/ljumptab.h
    ../../3rd/lua/llex.h 
    ../../3rd/lua/llimits.h 
    ../../3rd/lua/lmem.h 
    ../../3rd/lua/lobject.h 
    ../../3rd/lua/lopcodes.h
    ../../3rd/lua/lopnames.h     
    ../../3rd/lua/lparser.h
    ../../3rd/lua/lprefix.h    
    ../../3rd/lua/lstate.h 
    ../../3rd/lua/lstring.h 
    ../../3rd/lua/ltable.h 
    ../../3rd/lua/ltests.h 
    ../../3rd/lua/ltm.h 
    ../../3rd/lua/lua.h 
    ../../3rd/lua/luaconf.h 
    ../../3rd/lua/lualib.h
    ../../3rd/lua/lundump.h 
    ../../3rd/lua/lvm.h
    ../../3rd/lua/lzio.h
)

#SET_SOURCE_FILES_PROPERTIES(${HDR_LIBLUA} PROPERTIES HEADER_FILE_ONLY TRUE)
#include_directories(src)

# Build Libraries
SET (SRC_LIBLUA
    ../../3rd/lua/lapi.c
    ../../3rd/lua/lauxlib.c 
    ../../3rd/lua/lbaselib.c      
    ../../3rd/lua/lcode.c 
    ../../3rd/lua/lcorolib.c
    ../../3rd/lua/lctype.c 
    ../../3rd/lua/ldblib.c 
    ../../3rd/lua/ldebug.c 
    ../../3rd/lua/ldo.c 
    ../../3rd/lua/ldump.c 
    ../../3rd/lua/lfunc.c 
    ../../3rd/lua/lgc.c
    ../../3rd/lua/linit.c 
    ../../3rd/lua/liolib.c 
    ../../3rd/lua/llex.c 
    ../../3rd/lua/lmathlib.c 
    ../../3rd/lua/lmem.c 
    ../../3rd/lua/loadlib.c 
    ../../3rd/lua/lobject.c
    ../../3rd/lua/lopcodes.c 
    ../../3rd/lua/loslib.c 
    ../../3rd/lua/lparser.c 
    ../../3rd/lua/lstate.c 
    ../../3rd/lua/lstring.c 
    ../../3rd/lua/lstrlib.c
    ../../3rd/lua/ltable.c 
    ../../3rd/lua/ltablib.c 
    ../../3rd/lua/ltests.c 
    ../../3rd/lua/ltm.c 
    ../../3rd/lua/lundump.c 
    ../../3rd/lua/lutf8lib.c     
    ../../3rd/lua/lvm.c 
    ../../3rd/lua/lzio.c
)

SET ( SRC_LUA ../../3rd/lua/lua.c )
SET ( SRC_LUAC ../../3rd/lua/luac.c )

# compile with C++ compiler
set_source_files_properties(${SRC_LIBLUA} ${SRC_LUA} ${SRC_LUAC} PROPERTIES LANGUAGE CXX)

# append headers to sources to make them show up in MSVC GUI
LIST(APPEND SRC_LIBLUA ${HDR_LIBLUA})

set (SKYNET_SRC ../../skynet-src)
#Library
ADD_LIBRARY ( lualib ${SRC_LIBLUA} )
target_include_directories(lualib PRIVATE ${SKYNET_SRC})

#DLL
ADD_LIBRARY ( lua5.4.3 SHARED ${SRC_LIBLUA} )
target_include_directories(lua5.4.3 PRIVATE ${SKYNET_SRC})
SET_TARGET_PROPERTIES (lua5.4.3 PROPERTIES DEFINE_SYMBOL  "LUA_BUILD_AS_DLL" )

#exe
ADD_EXECUTABLE ( lua    ${SRC_LUA}  )
ADD_EXECUTABLE ( luac  ${SRC_LUAC} )

#lua uses a DLL; luac uses a library
TARGET_LINK_LIBRARIES ( lua lua5.4.3 )
TARGET_LINK_LIBRARIES ( luac lualib )