#if(TORQUE_SFX_OPENAL AND NOT TORQUE_DEDICATED)
    project(libtheora)
    file(GLOB LIBTHEORA_SOURCE_FILES "lib/*.c" "lib/*.h")
    file(GLOB LIBTHEORA_HEADER_FILES "include/theora/*.h") 
    set(LIBTHEORA_FILES ${LIBTHEORA_SOURCE_FILES} ${LIBTHEORA_HEADER_FILES}) 
    set(LIBTHEORA_COMPILE_DEFINES "")
    if (WIN32 AND TORQUE_CPU_X32)
        file(GLOB LIBTHEORA_SOURCE_FILES_X86_VC "lib/x86_vc/*.c")
        set(LIBTHEORA_FILES ${LIBTHEORA_FILES} ${LIBTHEORA_SOURCE_FILES_X86_VC})
        set(LIBTHEORA_COMPILE_DEFINES ${LIBTHEORA_COMPILE_DEFINES} OC_X86_ASM) 
    elseif (TORQUE_CPU_X32)
        file(GLOB LIBTHEORA_SOURCE_FILES_X86_VC "lib/x86/*.c")
        set(LIBTHEORA_FILES ${LIBTHEORA_FILES} ${LIBTHEORA_SOURCE_FILES_X86_VC})
        set(LIBTHEORA_COMPILE_DEFINES ${LIBTHEORA_COMPILE_DEFINES} OC_X86_ASM) 
    endif (WIN32 AND TORQUE_CPU_X32)

    add_library(libtheora ${LIBTHEORA_FILES})
    target_include_directories(libtheora PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
    target_link_libraries(libtheora PUBLIC libogg)
    target_compile_definitions(libtheora PUBLIC ${LIBTHEORA_COMPILE_DEFINES})
    set(TORQUE_INCLUDE_DIRECTORIES ${TORQUE_INCLUDE_DIRECTORIES} "${CMAKE_CURRENT_SOURCE_DIR}/include/theora")
    #set(TORQUE_LINK_LIBRARIES ${TORQUE_LINK_LIBRARIES} libtheora PARENT_SCOPE)
#endif()