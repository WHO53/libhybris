jb_sources = files(
  'dlfcn.c',
  'linker.c',
  'linker_environ.c',
  'linker_format.c',
  'rt.c',
  '../strlcpy.c'
)

jb_c_args = [
  '-DDEFAULT_HYBRIS_LD_LIBRARY_PATH="@0@"'.format(default_ld_path)
]

if arch == 'arm'
  jb_c_args += ['-DHAVE_ARM_TLS_REGISTER', '-DANDROID_ARM_LINKER']
elif arch == 'x86'
  jb_c_args += ['-DANDROID_X86_LINKER']
endif

if get_option('debug')
  jb_c_args += '-DLINKER_DEBUG=1'
else
  jb_c_args += '-DLINKER_DEBUG=0'
endif

if get_option('arm_tracing')
   jb_c_args += '-DWANT_ARM_TRACING'
endif

shared_module('jb',
  jb_sources,
  c_args : jb_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  name_prefix : '',
  install : true,
  install_dir : linker_plugin_dir
)
