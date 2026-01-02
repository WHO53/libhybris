linker_plugin_dir = join_paths(get_option('libdir'), 'libhybris', 'linker')

common_sources = files(
  'hooks.c',
  'hooks_shm.c',
  'strlcpy.c',
  'strlcat.c',
  'logging.c',
  'native_handle.c',
  'sysconf.c',
  'dso_handle_counters.cpp',
  'legacy_properties/properties.c',
  'legacy_properties/cache.c'
)

common_c_args = []
common_cpp_args = []

if get_option('property_cache')
  common_sources += files('legacy_properties/runtime_cache.c')
else
  common_c_args += '-DNO_RUNTIME_PROPERTY_CACHE'
endif

if get_option('arm_tracing')
  common_sources += files('wrappers.c', 'wrapper_code_generic_arm.c')
  common_c_args += '-DWANT_ARM_TRACING'
  common_cpp_args += '-DWANT_ARM_TRACING'
endif

common_defs = [
  '-DLINKER_PLUGIN_DIR="@0@"'.format(join_paths(get_option('prefix'), linker_plugin_dir)),
]

if get_option('adreno_quirks')
  common_defs += '-DWANT_ADRENO_QUIRKS'
endif

if get_option('trace')
  common_defs += '-DDEBUG'
endif

if get_option('mali_quirks')
  common_defs += '-DMALI_QUIRKS'
endif

if get_option('ubuntu_linker_overrides')
  common_defs += '-DUBUNTU_LINKER_OVERRIDES'
endif

if arch != 'arm64' and arch != 'x86_64'
   subdir('jb')
   common_defs += '-DWANT_LINKER_JB'
endif

if ver_major >= 6
  subdir('mm')
  common_defs += '-DWANT_LINKER_MM'
endif

if ver_major >= 7
  subdir('n')
  common_defs += '-DWANT_LINKER_N'
endif

if ver_major >= 8
  subdir('o')
  common_defs += '-DWANT_LINKER_O'
endif

if ver_major >= 10
  subdir('q')
  common_defs += '-DWANT_LINKER_Q'
endif

libhybris_common = shared_library('hybris-common',
  common_sources,
  c_args : common_c_args + common_defs,
  cpp_args : common_cpp_args + common_defs,
  include_directories : [hybris_inc, android_inc],
  dependencies : [dl_dep, rt_dep, thread_dep, android_headers_dep],
  install : true
)

libhybris_common_dep = declare_dependency(
  link_with : libhybris_common,
  include_directories : include_directories('.')
)