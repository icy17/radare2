r_arch_sources = [
  'arch.c',
  'arch_op.c',
  'arch_config.c',
  'arch_switch.c',
  'arch_session.c',
  'arch_cond.c',
  'arch_value.c',
  'p/null/plugin.c',
  'p/propeller/plugin.c',
  'p/propeller/propeller_disas.c',
  'p/arm/plugin.c',
  'p/arm/armass.c',
  'p/arm/armass64.c',
  'p/any_as/plugin.c',
  'p/any_vasm/plugin.c',
  'p/i4004/plugin.c',
  'p/amd29k/plugin.c',
  'p/jdh8/plugin.c',
  'p/pickle/plugin.c',
  'p/mcore/plugin.c',
  'p/mcore/mcore.c',
  'p/rsp/plugin.c',
  'p/rsp/rsp_idec.c',
  'p/riscv/plugin.c',
  'p/xap/plugin.c',
  'p/6502/plugin.c',
  'p/snes/plugin.c',
  'p/sh/plugin.c',
  'p/sh/gnu/sh-dis.c',
  'p/v810/plugin.c',
  'p/v810/v810_disas.c',
  'p/v850/plugin.c',
  'p/v850/v850dis.c',
  'p/v850/v850e0.c',
  'p/nios2/plugin.c',
  'p/nios2/nios2-opc.c',
  'p/nios2/nios2-dis.c',
]

# must be deleted when anal refactor is done
arch_inc = include_directories('../asm/arch/include')

r_arch = library('r_arch', r_arch_sources,
  include_directories: [platform_inc, arch_inc],
  c_args: library_cflags,
  dependencies: [
    r_util_dep,
    r_reg_dep,
    capstone_dep,
  ],
  install: true,
  implicit_include_directories: false,
  install_rpath: rpath_lib,
  soversion: r2_libversion
)

r_arch_dep = declare_dependency(link_with: r_arch,
                              include_directories: [platform_inc])

if get_option('blob')
r_arch_static = static_library('r_arch_static', r_arch_sources,
  include_directories: [platform_inc, arch_inc],
  c_args: library_cflags,
  dependencies: [
    r_util_static_dep,
    capstone_dep,
  ],
  install: true,
  implicit_include_directories: false,
)

r_arch_static_dep = declare_dependency(link_with: r_arch_static,
  include_directories: [platform_inc])
endif

pkgconfig_mod.generate(r_arch,
  subdirs: 'libr',
  version: r2_version,
  name: 'r_arch',
  filebase: 'r_arch',
  libraries: pkgcfg_sanitize_libs,
  requires: [
    'r_util',
    'r_reg',
  ],
  description: 'radare foundation libraries'
)
