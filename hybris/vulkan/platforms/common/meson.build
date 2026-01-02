vulkanplatformcommon_sources = files('vulkanplatformcommon.cpp')
vulkanplatformcommon_c_args = []
vulkanplatformcommon_cpp_args = []
vulkanplatformcommon_deps = [android_headers_dep]

if conf_data.get('WANT_WAYLAND', 0) == 1
  vulkanplatformcommon_deps += [wayland_dep, wayland_server_dep]
endif

if get_option('trace')
  vulkanplatformcommon_c_args += '-DDEBUG'
  vulkanplatformcommon_cpp_args += '-DDEBUG'
endif

libhybris_vulkanplatformcommon = shared_library('hybris-vulkanplatformcommon',
  vulkanplatformcommon_sources,
  c_args : vulkanplatformcommon_c_args,
  cpp_args : vulkanplatformcommon_cpp_args,
  include_directories : [hybris_inc, 
    vulkan_inc,
    platform_common_inc,
    android_inc
  ],
  dependencies : vulkanplatformcommon_deps,
  link_with : [libhybris_common, libhybris_platformcommon],
  version : '1.0.0',
  install : true
)

libhybris_vulkanplatformcommon_dep = declare_dependency(
  link_with : libhybris_vulkanplatformcommon,
  include_directories : include_directories('.')
)
