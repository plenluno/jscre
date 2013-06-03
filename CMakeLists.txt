# Copyright (c) 2013 Plenluno All rights reserved.

cmake_minimum_required(VERSION 2.8)

project(jscre)

# variables --------------------------------------------------------------------

## jscre-src
set(jscre-src
    pcre_compile.cpp
    pcre_exec.cpp
    pcre_tables.cpp
    pcre_ucp_searchfuncs.cpp
    pcre_xclass.cpp
)

## jscre-cflags
if(UNIX)
    set(jscre-cflags
        -fno-rtti
        -fno-exceptions
    )

    if(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
        set(jscre-cflags
            ${jscre-cflags}
            -Wno-null-conversion
            -Wno-null-dereference
        )
    else(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
        set(jscre-cflags
            ${jscre-cflags}
            -Wno-conversion-null
        )
    endif(CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
else(UNIX)
    set(jscre-cflags
        /W1
    )
endif(UNIX)

string(REPLACE ";" " " jscre-cflags "${jscre-cflags}")

# build ------------------------------------------------------------------------

add_library(jscre STATIC
    ${jscre-src}
)

set_target_properties(jscre PROPERTIES
    COMPILE_FLAGS "${jscre-cflags}"
)
