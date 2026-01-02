mm_sources = files(
  'hybris_compat.cpp',
  'dlfcn.cpp',
  'linker_allocator.cpp',
  'linker_block_allocator.cpp',
  'linker.cpp',
  'linker_memory.cpp',
  'linker_phdr.cpp',
  'linker_sdk_versions.cpp',
  'rt.cpp',
  '../strlcpy.c',
  '../strlcat.c'
)

mm_args = [
  '-DDEFAULT_HYBRIS_LD_LIBRARY_PATH="@0@"'.format(default_ld_path),
  '-DTRACE_DEBUG=1',
  '-fno-stack-protector',
  '-Wstrict-overflow=5'
]

if get_option('arm_tracing')
   mm_args += '-DWANT_ARM_TRACING'
endif

shared_module('mm',
  mm_sources,
  cpp_args : mm_args,
  c_args : mm_args,
  include_directories : [hybris_inc,
      include_directories('bionic/libc'),
      include_directories('bionic/libc/include'),
      android_inc],
  dependencies : [android_headers_dep],
  link_args : ['-lsupc++'],
  install : true,
  install_dir : linker_plugin_dir
)
