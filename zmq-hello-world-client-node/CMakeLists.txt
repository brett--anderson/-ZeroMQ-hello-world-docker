cmake_minimum_required(VERSION 3.6)
project(zmq_hello_world)

set(CMAKE_CXX_STANDARD 11)

## load in pkg-config support
find_package(PkgConfig)
## use pkg-config to get hints for 0mq locations
pkg_check_modules(PC_ZeroMQ QUIET zmq)

## use the hint from about to find the location of libzmq
find_library(ZeroMQ_LIBRARY
        NAMES zmq
        PATHS ${PC_ZeroMQ_LIBRARY_DIRS}
        )

set(SOURCE_FILES
        src/hwclient.c)

add_executable(zmq_hello_world ${SOURCE_FILES})

## at the 0mq library to our link directive
target_link_libraries(zmq_hello_world PUBLIC ${ZeroMQ_LIBRARY})