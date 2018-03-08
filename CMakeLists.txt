cmake_minimum_required(VERSION 2.8)

option(SOFTUART_DEBUG "Enable debug." OFF)
option(USE_STATIC_SOFTUART_LIBRARY "Build softuart static library." OFF)
option(USE_OBJECT_SOFTUART_LIBRARY "Build softuart object library." ON)

file(WRITE "${CMAKE_BINARY_DIR}/softuart/user_config.h"
    "#ifndef __USER_CONFIG_H__\n"
    "#define __USER_CONFIG_H__\n"
    "#endif\n"
)

if(SOFTUART_DEBUG)
    add_definitions(-DSOFTUART_DEBUG)
endif(SOFTUART_DEBUG)

include_directories(esp8266-software-uart/softuart/include
                    ${CMAKE_BINARY_DIR}/softuart)

if(USE_OBJECT_SOFTUART_LIBRARY)
    add_library(softuart-object OBJECT esp8266-software-uart/softuart/softuart.c)
endif(USE_OBJECT_SOFTUART_LIBRARY)

if(USE_STATIC_SOFTUART_LIBRARY)
    add_library(softuart-static STATIC esp8266-software-uart/softuart/softuart.c)
    # target_compile_definitions(json-jsmn-object PRIVATE MQTT_SERVER MQTT_CLIENT)
endif(USE_STATIC_SOFTUART_LIBRARY)
