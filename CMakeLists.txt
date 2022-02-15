cmake_minimum_required(VERSION 2.6)
PROJECT(CLIENT)
aux_source_directory(. DIR_SRCS)
add_subdirectory(rcssbase)
add_executable(client ${DIR_SRCS}) 

target_link_libraries(client NET)
target_link_libraries(client GZIP)
