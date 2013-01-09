cmake_minimum_required(VERSION 2.8)

project(jscre)

# variables ----------------------------------------------------------------------------------------

## jscre-src
set(jscre-src
    pcre_compile.cpp
    pcre_exec.cpp
    pcre_tables.cpp
    pcre_ucp_searchfuncs.cpp
    pcre_xclass.cpp
)

## jscre-cflags
set(jscre-cflags
    -fno-rtti
    -fno-exceptions
    -Wno-null-dereference
)

string(REPLACE ";" " " jscre-cflags "${jscre-cflags}")

# build --------------------------------------------------------------------------------------------

add_library(jscre STATIC
    ${jscre-src}
)

set_target_properties(jscre PROPERTIES
    COMPILE_FLAGS "${jscre-cflags}"
)
