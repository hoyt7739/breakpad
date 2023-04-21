project(dump_syms)

if(WIN32)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /I\"$(VSInstallDir)DIA SDK/include\"")
    set(CMAKE_C_FLAGS ${CMAKE_CXX_FLAGS})
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /LIBPATH:\"$(VSInstallDir)DIA SDK/lib\"")
    set(SOURCES
        ${COMMON_DIR}/windows/string_utils.cc
        ${COMMON_DIR}/windows/guid_string.cc
        ${COMMON_DIR}/windows/dia_util.cc
        ${COMMON_DIR}/windows/omap.cc
        ${COMMON_DIR}/windows/pe_util.cc
        ${COMMON_DIR}/windows/pe_source_line_writer.cc
        ${COMMON_DIR}/windows/pdb_source_line_writer.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/windows/dump_syms/dump_syms.cc)
    set(LIBRARIES
        diaguids
        Dbghelp
        ImageHlp)
elseif(UNIX)
    set(SOURCES
        ${COMMON_DIR}/dwarf_cfi_to_module.cc
        ${COMMON_DIR}/dwarf_cu_to_module.cc
        ${COMMON_DIR}/dwarf_line_to_module.cc
        ${COMMON_DIR}/dwarf_range_list_handler.cc
        ${COMMON_DIR}/language.cc
        ${COMMON_DIR}/module.cc
        ${COMMON_DIR}/path_helper.cc
        ${COMMON_DIR}/stabs_reader.cc
        ${COMMON_DIR}/stabs_to_module.cc
        ${COMMON_DIR}/dwarf/bytereader.cc
        ${COMMON_DIR}/dwarf/dwarf2diehandler.cc
        ${COMMON_DIR}/dwarf/dwarf2reader.cc
        ${COMMON_DIR}/dwarf/elf_reader.cc
        ${COMMON_DIR}/linux/crc32.cc
        ${COMMON_DIR}/linux/dump_symbols.cc
        ${COMMON_DIR}/linux/elf_symbols_to_module.cc
        ${COMMON_DIR}/linux/elfutils.cc
        ${COMMON_DIR}/linux/file_id.cc
        ${COMMON_DIR}/linux/linux_libc_support.cc
        ${COMMON_DIR}/linux/memory_mapped_file.cc
        ${COMMON_DIR}/linux/safe_readlink.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/linux/dump_syms/dump_syms.cc)
    set(LIBRARIES
        z)
endif()

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR})

target_link_libraries(${PROJECT_NAME} ${LIBRARIES})
