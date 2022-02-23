cmake_minimum_required(VERSION 3.5)

project(client VERSION 0.1.1)

aux_source_directory(${PROJECT_SOURCE_DIR}/rcssbase/net NET )
aux_source_directory(${PROJECT_SOURCE_DIR}/rcssbase/gzip GZIP )

add_definitions(-DHAVE_CONFIG_H)

add_executable(
    ${PROJECT_NAME} 
    ${NET}
    ${GZIP}
    client.cpp 
    )

target_include_directories(client 
    PUBLIC
    ${PROJECT_SOURCE_DIR}
    ${PROJECT_SOURCE_DIR}/rcssbase/net
    ${PROJECT_SOURCE_DIR}/rcssbase/gzip

)
    

# check boost
find_package(Boost 1.38.0 COMPONENTS program_options system REQUIRED)
if(Boost_PROGRAM_OPTIONS_FOUND)
  set(HAVE_BOOST_PROGRAM_OPTIONS TRUE)
endif()

# check zlib
find_package(ZLIB)
if(ZLIB_FOUND)
  set(HAVE_LIBZ TRUE)
endif()

target_link_libraries(client 
    PUBLIC
    Boost::system
    ZLIB::ZLIB
)

# install(TARGETS client DESTINATION bin)

