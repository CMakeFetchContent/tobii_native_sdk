cmake_minimum_required(VERSION 3.15)
project(tobii_stream_engine)

# Tobii Native SDK
add_library( tobii_stream_engine SHARED IMPORTED GLOBAL )
if(ANDROID)
    set_target_properties( tobii_stream_engine PROPERTIES 
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/stream_engine/lib/Android/${CMAKE_ANDROID_ARCH_ABI}/libtobii_stream_engine.so 
    )     
elseif(WIN32) 
    set_target_properties( tobii_stream_engine PROPERTIES 
        IMPORTED_IMPLIB ${CMAKE_CURRENT_SOURCE_DIR}/stream_engine/lib/x86_64/tobii_stream_engine.lib 
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/stream_engine/lib/x86_64/tobii_stream_engine.dll 
    )      
else()
    set_target_properties( tobii_stream_engine PROPERTIES 
        IMPORTED_LOCATION ${CMAKE_CURRENT_SOURCE_DIR}/stream_engine/lib/x86_64/libtobii_stream_engine.so 
    )      
endif()
target_include_directories( tobii_stream_engine 
    INTERFACE
        ${CMAKE_CURRENT_LIST_DIR}/stream_engine/include
)