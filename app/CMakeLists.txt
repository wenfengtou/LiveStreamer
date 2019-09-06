cmake_minimum_required(VERSION 3.4.2)

set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -D_DEBUG -D_LIB")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D_DEBUG -D_LIB")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall")


include_directories(src/main/cpp/BasicUsageEnvironment/include)
include_directories(src/main/cpp/groupsock/include)
include_directories(src/main/cpp/liveMedia/include)
include_directories(src/main/cpp/LiveStreamer/include)
include_directories(src/main/cpp/mediaServer/include)
include_directories(src/main/cpp/UsageEnvironment/include)

file(GLOB_RECURSE BasicUsageEnvironment "src/main/cpp/BasicUsageEnvironment/*")
file(GLOB_RECURSE groupsock "src/main/cpp/groupsock/*")
file(GLOB_RECURSE liveMedia "src/main/cpp/liveMedia/*")
file(GLOB_RECURSE LiveStreamer "src/main/cpp/LiveStreamer/*")
file(GLOB_RECURSE mediaServer "src/main/cpp/mediaServer/*")
file(GLOB_RECURSE UsageEnvironment "src/main/cpp/UsageEnvironment/*")


add_library(LiveStreamer
        SHARED
        ${BasicUsageEnvironment}
        ${groupsock}
        ${liveMedia}
        ${LiveStreamer}
        ${mediaServer}
        ${UsageEnvironment}
        )

find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)


target_link_libraries( # Specifies the target library.
        LiveStreamer
        ${log-lib})

