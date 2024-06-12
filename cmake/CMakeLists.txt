project(skynet-Win)
option(LUA_CLIB_PATH, "luaclib")
option(CSERVICE_PATH, "cservice")

option(SKYNET_BUILD_PATH, ".")

option(TLS_LIB "");
option(TLS_INC "");


option(JEMALLOC_STATICLIB "3rd/jemalloc/lib/");
option(JEMALLOC_INC "3rd/jemalloc/include/jemalloc");

#cmake doc https://cmake-doc.readthedocs.io/zh-cn/latest/index.html
#libName
#libInclude
#libpath

set(LUA_STATICLIB , "3rd/lua/liblua.a")
option(LUA_LIB ${LUA_STATICLIB})
option(LUA_INC "3rd/lua")

add_library(lualib STATIC IMPORTED)
add_library(jemalloc STATIC IMPORTED)
add_library(tlslib STATIC IMPORTED)

#lua

set(CFLAGS -g -O2 -Wall -I${SKYNET_BUILD_PATH}/skynet-src)
add_library(${LUA_STATICLIB} STATIC ${LUASTATIC_SRC})

set(SKYNET_SRC
     ../skynet-src/skynet_main.c
     ../skynet-src/skynet_handle.c
     ../skynet-src/skynet_module.c
     ../skynet-src/skynet_mq.c
     ../skynet-src/skynet_server.c
     ../skynet-src/skynet_start.c
     ../skynet-src/skynet_timer.c
     ../skynet-src/skynet_error.c
     ../skynet-src/skynet_harbor.c
     ../skynet-src/skynet_env.c
     ../skynet-src/skynet_monitor.c
     ../skynet-src/skynet_socket.c
     ../skynet-src/socket_server.c
     ../skynet-src/malloc_hook.c
     ../skynet-src/skynet_daemon.c
     ../skynet-src/skynet_log.c
)

add_executable(skynet ${SKYNET_SRC})
target_link_libraries(skynet lualib jemalloc tlslib)
target_include_directories(skynet ${LUA_INC})

target_include_directories(skynet ${JEMALLOC_INC})

target_include_directories(skynet ${TLS_INC})
