
add_subdirectory(gzip)
add_subdirectory(net)

aux_source_directory(/gzip/. DIR_GZIP_SRCS)
aux_source_directory(/net/. DIR_NET_SRCS)
 
add_library(GZIP ${DIR_GZIP_SRCS})
add_library(NET ${DIR_NET_SRCS})
