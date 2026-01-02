n_sources = files(
  'hybris_compat.cpp',
  'dlfcn.cpp',
  'linker_allocator.cpp',
  'linker_block_allocator.cpp',
  'linker.cpp',
  'linker_dlwarning.cpp',
  'linker_gdb_support.cpp',
  'linker_mapped_file_fragment.cpp',
  'linker_memory.cpp',
  'linker_phdr.cpp',
  'linker_sdk_versions.cpp',
  'linker_utils.cpp',
  'rt.cpp',
  '../strlcpy.c',
  '../strlcat.c'
)

n_args = [
  '-DDEFAULT_HYBRIS_LD_LIBRARY_PATH="@0@"'.format(default_ld_path),
  '-DTRACE_DEBUG=1',
  '-fno-stack-protector',
  '-Wstrict-overflow=5'
]

if get_option('arm_tracing')
   n_args += '-DWANT_ARM_TRACING'
endif

shared_module('n',
  n_sources,
  cpp_args : n_args,
  c_args : n_args,
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
