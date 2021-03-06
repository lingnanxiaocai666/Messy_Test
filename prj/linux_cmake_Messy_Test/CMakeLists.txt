PROJECT(Messy_Test)
CMAKE_MINIMUM_REQUIRED(VERSION 3.0)

# support C++11
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -Wall -O2 -std=c11")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -g -Wall -O2 -std=c++11")
# suport C++14, when gcc version > 5.1, use -std=c++14 instead of c++1y
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -g -Wall -O2 -std=c++1y")

MESSAGE(STATUS "project source dir: ${PROJECT_SOURCE_DIR}")
SET(PATH_TEST_FILES ${PROJECT_SOURCE_DIR}/./../../demo/Messy_Test)
SET(PATH_YAML_CPP_FILES ${PROJECT_SOURCE_DIR}/./../../src/yaml-cpp)
SET(PATH_RAPIDJSON_FILES ${PROJECT_SOURCE_DIR}/./../../src/rapidjson)
SET(PATH_LIBUUID_FILES ${PROJECT_SOURCE_DIR}/./../../src/libuuid)
SET(PATH_TINYXML2_FILES ${PROJECT_SOURCE_DIR}/./../../src/tinyxml2)
SET(PATH_JEMALLOC_FILES ${PROJECT_SOURCE_DIR}/./../../src/jemalloc)

# head files search path
INCLUDE_DIRECTORIES(
	${PATH_TEST_FILES}
	${PATH_YAML_CPP_FILES}/include
	${PATH_RAPIDJSON_FILES}/include
	${PATH_LIBUUID_FILES}
	${PATH_TINYXML2_FILES}
	${PATH_JEMALLOC_FILES}/build/include
)

LINK_DIRECTORIES(${PROJECT_SOURCE_DIR}/build)

# recursive query match files :*.cpp
FILE(GLOB_RECURSE CPP_TEST_LIST ${PATH_TEST_FILES}/*.cpp)
SET(CPP_TINYXML2_SRC ${PROJECT_SOURCE_DIR}/./../../src/tinyxml2/tinyxml2.cpp)

# build executable program
ADD_EXECUTABLE(Messy_Test ${CPP_TEST_LIST} ${CPP_TINYXML2_SRC})
# add dependent library: static and dynamic
TARGET_LINK_LIBRARIES(Messy_Test yaml-cpp uuid jemalloc dl pthread)

