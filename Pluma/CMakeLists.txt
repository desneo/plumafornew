cmake_minimum_required(VERSION 3.15)

project(pluma)

set(CMAKE_CXX_STANDARD 17)

if(WIN32)
    # 解决msvc下编译文件格式的问题
    add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
    add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")
endif()

set(SOURCE_HEAD ${CMAKE_CURRENT_SOURCE_DIR}/include)
set(SOURCE_CPP ${CMAKE_CURRENT_SOURCE_DIR}/src)

include_directories(
    ${SOURCE_HEAD}
    ${SOURCE_HEAD}/Pluma
    ${SOURCE_CPP}
    ${SOURCE_CPP}/Pluma
    )

aux_source_directory(${SOURCE_CPP}/Pluma PlumaStaticSRC)

# add_library(${PROJECT_NAME} STATIC ${PlumaStaticSRC})
add_library(${PROJECT_NAME} SHARED ${PlumaStaticSRC})
set_target_properties(${PROJECT_NAME} PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS TRUE)

# add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/example)
