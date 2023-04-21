project(minidump_stackwalk)

set(SOURCES
    ${THIRD_PARTY_DIR}/libdisasm/ia32_implicit.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_insn.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_invariant.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_modrm.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_opcode_tables.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_operand.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_reg.c
    ${THIRD_PARTY_DIR}/libdisasm/ia32_settings.c
    ${THIRD_PARTY_DIR}/libdisasm/x86_disasm.c
    ${THIRD_PARTY_DIR}/libdisasm/x86_format.c
    ${THIRD_PARTY_DIR}/libdisasm/x86_imm.c
    ${THIRD_PARTY_DIR}/libdisasm/x86_insn.c
    ${THIRD_PARTY_DIR}/libdisasm/x86_misc.c
    ${THIRD_PARTY_DIR}/libdisasm/x86_operand_list.c
    ${COMMON_DIR}/path_helper.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/basic_code_modules.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/basic_source_line_resolver.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/call_stack.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/cfi_frame_info.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/convert_old_arm64_context.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/disassembler_x86.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/dump_context.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/dump_object.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/exploitability.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/exploitability_linux.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/exploitability_win.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/logging.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/minidump.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/minidump_processor.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/pathname_stripper.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/process_state.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/proc_maps_linux.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/simple_symbol_supplier.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/source_line_resolver_base.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stack_frame_cpu.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stack_frame_symbolizer.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalk_common.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_address_list.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_amd64.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_arm.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_arm64.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_mips.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_ppc.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_ppc64.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_riscv.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_riscv64.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_sparc.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/stackwalker_x86.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/symbolic_constants_win.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/tokenize.cc
    ${CMAKE_CURRENT_SOURCE_DIR}/minidump_stackwalk.cc)

if(UNIX)
    list(APPEND SOURCES
        ${COMMON_DIR}/linux/scoped_pipe.cc
        ${COMMON_DIR}/linux/scoped_tmpfile.cc
        ${CMAKE_CURRENT_SOURCE_DIR}/disassembler_objdump.cc)
endif()

add_executable(${PROJECT_NAME} ${SOURCES})

target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR})
