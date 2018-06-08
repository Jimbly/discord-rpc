cmake_minimum_required (VERSION 3.1)

project (discord)

include (../../Tools/LinuxBuild/shared.cmake)

include_directories (${CMAKE_CURRENT_SOURCE_DIR}/../)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/../libs)

include_directories(include deps/rapidjson-1.1.0/include)

if (EX_TARGET_OS STREQUAL "Darwin")
	file(GLOB MySRC
		"${CMAKE_CURRENT_SOURCE_DIR}/src/connection_unix.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/discord_register_osx.m" # Only on OSX
		"${CMAKE_CURRENT_SOURCE_DIR}/src/discord_register_linux.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/discord_rpc.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_connection.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/serialization.cpp"
	)
else ()
	file(GLOB MySRC
		"${CMAKE_CURRENT_SOURCE_DIR}/src/connection_unix.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/discord_register_linux.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/discord_rpc.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/rpc_connection.cpp"
		"${CMAKE_CURRENT_SOURCE_DIR}/src/serialization.cpp"
	)
endif ()

add_library (${PROJECT_NAME} STATIC ${MySRC})
set_target_properties (${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}${EX_PLATFORM}" PREFIX "")
