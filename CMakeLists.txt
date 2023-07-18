cmake_minimum_required(VERSION 3.18)

project(tinySAK)

add_definitions(-DTINYSAK_IMPORTS_IGNORE)

if (BUILD_SHARED_LIBS)
  add_definitions(-DTINYSAK_EXPORTS)
endif ()

if(UNIX)
    if(NOT APPLE)
        add_link_options("LINKER:--exclude-libs,ALL" "LINKER:--as-needed")
        set(CMAKE_POSITION_INDEPENDENT_CODE ON)
    endif()
    add_compile_options(-fvisibility=hidden)
endif()

include_directories(${CMAKE_CURRENT_LIST_DIR}/src)

file(GLOB_RECURSE TINY_NET_SOURCE src/*.h src/*.c)

add_library(${PROJECT_NAME} ${TINY_NET_SOURCE})

if (BUILD_SHARED_LIBS)
  if (WIN32)
    target_link_libraries(${PROJECT_NAME} Winmm)
  endif ()
endif ()
