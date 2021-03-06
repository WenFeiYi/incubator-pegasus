# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.

set(MY_PROJ_NAME "pegasus_shell")
project(${MY_PROJ_NAME} C CXX)

# Source files under CURRENT project directory will be automatically included.
# You can manually set MY_PROJ_SRC to include source files under other directories.
set(MY_PROJ_SRC "linenoise/linenoise.c" "sds/sds.c")

# Search mode for source files under CURRENT project directory?
# "GLOB_RECURSE" for recursive search
# "GLOB" for non-recursive search
set(MY_SRC_SEARCH_MODE "GLOB_RECURSE")

set(MY_PROJ_LIBS
    pegasus_base
    dsn.replication.tool
    dsn_replica_server
    dsn_replication_common
    dsn_client
    dsn_utils
    dsn.block_service.local
    dsn.block_service.fds
    dsn.block_service
    dsn.failure_detector
    pegasus_client_static
    galaxy-fds-sdk-cpp
    PocoNet
    PocoFoundation
    PocoNetSSL
    PocoJSON
    pegasus_geo_lib
    RocksDB::rocksdb
    s2
    )

set(MY_BINPLACES "${CMAKE_CURRENT_SOURCE_DIR}/config.ini")

set(MY_BOOST_LIBS
    Boost::system
    Boost::filesystem 
    Boost::regex # dsn_replica_server.so needs
    )

SET(CMAKE_INSTALL_RPATH ".")
SET(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)

add_definitions(-Wno-attributes)

dsn_add_executable()
dsn_install_executable()
