cmake_minimum_required(VERSION 2.6)
PROJECT(CLIENT)

aux_source_directory(. DIR_SRCS)
aux_source_directory(${PROJECT_SOURCE_DIR}/rcssbase/gzip GZIP)
aux_source_directory(${PROJECT_SOURCE_DIR}/rcssbase/net  NET)

add_executable(client ${DIR_SRCS} ${GZIP} ${NET}) 

add_definitions(-DHAVE_CONFIG_H)

target_include_directories(client
    PUBLIC
    ${PROJECT_SOURCE_DIR}
    ${PROJECT_SOURCE_DIR}/rcssbase/gzip
    ${PROJECT_SOURCE_DIR}/rcssbase/net
    )

# boost
find_package(Boost 1.36.0 COMPONENTS system REQUIRED)
if(NOT Boost_FOUND)
  message(FATAL_ERROR "Boost not found!")
endif()

# zlib
find_package(ZLIB)
if(ZLIB_FOUND)
  #add_definitions(-DHAVE_LIBZ)
  set(HAVE_LIBZ TRUE)
endif()

target_link_libraries(client
    PUBLIC
    Boost::system
    ZLIB::ZLIB
  )
