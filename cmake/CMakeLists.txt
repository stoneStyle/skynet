option(LUA_CLIB_PATH, "luaclib")
option(CSERVICE_PATH, "cservice")

option(SKYNET_BUILD_PATH, ".")

#lua
set(LUA_STATICLIB , "3rd/lua/liblua.a")
option(LUA_LIB ${LUA_STATICLIB})
option(LUA_INC "3rd/lua")

set(CFLAGS -g -O2 -Wall -I${SKYNET_BUILD_PATH}/skynet-src)

set(LUASTATIC_SRC 
        3rd/lua/lapi.c 
        3rd/lua/lauxlib.c 
        3rd/lua/lbaselib.c
        3rd/lua/lcode.c 
        3rd/lua/lcorolib.c 
        3rd/lua/lctype.c 
        3rd/lua/ldblib.c 
        3rd/lua/ldebug.c 
        3rd/lua/ldo.c 
        3rd/lua/ldump.c 
        3rd/lua/lfunc.c 
        3rd/lua/lgc.c 
        3rd/lua/linit.c 
        3rd/lua/liolib.c
        3rd/lua/llex.c
        3rd/lua/lmathlib.c 
        3rd/lua/lmem.c 
        3rd/lua/loadlib.c 
        3rd/lua/lobject.c 
        3rd/lua/lopcodes.c 
        3rd/lua/loslib.c 
        3rd/lua/lparser.c 
        3rd/lua/lstate.c 
        3rd/lua/lstring.c 
        3rd/lua/lstrlib.c 
        3rd/lua/ltable.c 
        3rd/lua/ltablib.c 
        3rd/lua/ltests.c 
        3rd/lua/ltm.c          
        3rd/lua/lundump.c
        3rd/lua/lvm.c
         3rd/lua/lzio.c)

add_library(${LUA_STATICLIB} STATIC ${LUASTATIC_SRC})