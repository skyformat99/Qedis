#PROJECT(QEDISSERVER)

INCLUDE(${PROJECT_SOURCE_DIR}/CMakeCommon)

AUX_SOURCE_DIRECTORY(. QEDISSERVER_SRC)

LINK_DIRECTORIES(../../leveldb)
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/QBase; ${PROJECT_SOURCE_DIR}/QedisCore)

ADD_EXECUTABLE(qedis_server ${QEDISSERVER_SRC})
SET(EXECUTABLE_OUTPUT_PATH  ../../bin)

TARGET_LINK_LIBRARIES(qedis_server qediscore; qbaselib; leveldb)
ADD_DEPENDENCIES(qedis_server qbaselib; qediscore; leveldb)
IF(${QEDIS_CLUSTER} EQUAL 1)
    INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/QCluster)
    TARGET_LINK_LIBRARIES(qedis_server qcluster)
    ADD_DEPENDENCIES(qedis_server qcluster)
ENDIF()

