o_sources = files(
  'hybris_compat.cpp',
  'dlfcn.cpp',
  'linker_allocator.cpp',
  'linker_block_allocator.cpp',
  'linker.cpp',
  'linker_cfi.cpp',
  'linker_config.cpp',
  'linker_dlwarning.cpp',
  'linker_gdb_support.cpp',
  'linker_globals.cpp',
  'linker_logger.cpp',
  'linker_main.cpp',
  'linker_mapped_file_fragment.cpp',
  'linker_memory.cpp',
  'linker_namespaces.cpp',
  'linker_phdr.cpp',
  'linker_sdk_versions.cpp',
  'linker_soinfo.cpp',
  'linker_utils.cpp',
  'rt.cpp',
  '../strlcpy.c',
  '../strlcat.c'
)

o_args = [
  '-DDEFAULT_HYBRIS_LD_LIBRARY_PATH="@0@"'.format(default_ld_path),
  '-DTRACE_DEBUG=1',
  '-fno-stack-protector',
  '-Wstrict-overflow=5'
]

if ver_major >= 9
  o_args += '-DHAS_ANDROID_9_0_0'
endif

if get_option('arm_tracing')
   o_args += '-DWANT_ARM_TRACING'
endif

shared_module('o',
  o_sources,
  cpp_args : o_args,
  c_args : o_args,
  include_directories : [hybris_inc,
      include_directories('bionic/libc'),
      include_directories('bionic/libc/include'),
      android_inc],
  dependencies : [android_headers_dep],
  link_args : ['-lsupc++'],
  name_prefix : '',
  install : true,
  install_dir : linker_plugin_dir
)
