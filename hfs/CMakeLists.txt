INCLUDE(FindZLIB)

IF(NOT ZLIB_FOUND)
	message(FATAL_ERROR "zlib is required for hfs!")
ENDIF(NOT ZLIB_FOUND)

include_directories(${ZLIB_INCLUDE_DIR})

link_directories(${PROJECT_BINARY_DIR}/common)
add_library(hfs btree.c catalog.c extents.c xattr.c fastunicodecompare.c flatfile.c hfslib.c rawfile.c utility.c volume.c hfscompress.c)
target_link_libraries(hfs common ${ZLIB_LIBRARIES})

add_executable(hfsplus hfs.c)
target_link_libraries(hfsplus hfs)

install(TARGETS hfsplus DESTINATION bin)

