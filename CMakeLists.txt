PROJECT(rtunnel-cpp)

cmake_minimum_required(VERSION 2.8)
cmake_policy(SET CMP0015 NEW)

SET(CMAKE_VERBOSE_MAKEFILE ON)

SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")

IF(CMAKE_COMPILER_IS_GNUCC)
  SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fmessage-length=0")
ENDIF(CMAKE_COMPILER_IS_GNUCC)

IF(CMAKE_COMPILER_IS_GNUCXX)
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fmessage-length=0")
ENDIF(CMAKE_COMPILER_IS_GNUCXX)

add_subdirectory(common lib)

link_directories(${PROJECT_BINARY_DIR}/lib)

aux_source_directory(server SERVER_SRCS)

aux_source_directory(client CLIENT_SRCS)

ADD_EXECUTABLE(rtunnel-server
    ${SERVER_SRCS}
)

ADD_EXECUTABLE(rtunnel-client
    ${CLIENT_SRCS}
)

target_link_libraries(rtunnel-server rtunnel-common)
