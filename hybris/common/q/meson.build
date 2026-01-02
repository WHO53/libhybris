q_sources = files(
  'hybris_compat.cpp',
  'bionic/libc/bionic/bionic_call_ifunc_resolver.cpp',
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
  'linker_tls.cpp',
  'linker_utils.cpp',
  'rt.cpp',
  '../strlcpy.c',
  '../strlcat.c',
  'bionic/libc/bionic/bionic_elf_tls.cpp',
  'bionic/libc/bionic/bionic_allocator.cpp'
)

if arch == 'arm64'
  q_sources += files('tlsdesc_resolver.S')
endif

q_args = [
  '-DDEFAULT_HYBRIS_LD_LIBRARY_PATH="@0@"'.format(default_ld_path),
  '-D_USING_LIBCXX',
  '-DTRACE_DEBUG=1',
  '-fno-stack-protector',
  '-Wstrict-overflow=5'
]

if ver_major >= 11
  q_args += '-DHAS_ANDROID_11_0_0'
endif

if get_option('arm_tracing')
   q_args += '-DWANT_ARM_TRACING'
endif

shared_module('q',
  q_sources,
  cpp_args : q_args,
  c_args : q_args,
  include_directories : [hybris_inc,
      include_directories('bionic/libc'),
      include_directories('bionic/libc/include'),
      android_inc],
  dependencies : [android_headers_dep],
  link_args : ['-lsupc++', '-lpthread'],
  name_prefix : '',
  install : true,
  install_dir : linker_plugin_dir
)
