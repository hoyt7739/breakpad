project(exception_handler)

if(WIN32)
    set(SOURCES
        ${COMMON_DIR}/windows/guid_string.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/windows/crash_generation/crash_generation_client.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/windows/handler/exception_handler.cc)
elseif(UNIX)
    set(SOURCES
        ${COMMON_DIR}/md5.cc
        ${COMMON_DIR}/string_conversion.cc
        ${COMMON_DIR}/convert_UTF.cc
        ${COMMON_DIR}/linux/elfutils.cc
        ${COMMON_DIR}/linux/file_id.cc
        ${COMMON_DIR}/linux/guid_creator.cc
        ${COMMON_DIR}/linux/linux_libc_support.cc
        ${COMMON_DIR}/linux/memory_mapped_file.cc
        ${COMMON_DIR}/linux/safe_readlink.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/minidump_file_writer.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/microdump_writer/microdump_writer.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/crash_generation/crash_generation_client.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/dump_writer_common/thread_info.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/dump_writer_common/ucontext_reader.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/log/log.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/minidump_writer/pe_file.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/minidump_writer/linux_core_dumper.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/minidump_writer/linux_dumper.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/minidump_writer/linux_ptrace_dumper.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/minidump_writer/minidump_writer.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/handler/exception_handler.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/handler/minidump_descriptor.cc)
endif()

add_library(${PROJECT_NAME} STATIC ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR})
