# If not stated otherwise in this file or this component's license file the
# following copyright and licenses apply:
#
# Copyright 2020 Metrological
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

find_package(GTest REQUIRED)

# TODO: coverage causes attempt to write on invalid location, -keep-static-functions is not recognized by buildroot compiler
set(CMAKE_CPP_FLAGS "${CMAKE_CPP_FLAGS} --coverage -fno-inline -fno-inline-small-functions -fno-default-inline -I${PARENT_DIR}/Source")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pthread")

SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -fprofile-arcs")

#set(GTEST_INCLUDE_DIR /usr/include/gtest)

if(NOT APPLE)
    include_directories(${GTEST_INCLUDE_DIR})
endif()

SET(BASEPATH "${CMAKE_SOURCE_DIR}")

include_directories(${BASEPATH}/Source)

set(CMAKE_CXX_STANDARD 11)

enable_testing()

add_subdirectory(core)
add_subdirectory(tests)
