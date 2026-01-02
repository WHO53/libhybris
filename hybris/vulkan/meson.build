vulkan_sources = files('vulkan.c', 'ws.c')
vulkan_c_args = [
  '-DPKGLIBDIR="@0@"'.format(join_paths(get_option('prefix'), get_option('libdir'), 'libhybris'))
]
if get_option('trace')
  vulkan_c_args += '-DDEBUG'
endif

libvulkan = shared_library('vulkan',
  vulkan_sources,
  c_args : vulkan_c_args,
  include_directories : [hybris_inc, 
    android_inc
  ],
  dependencies : [android_headers_dep, dl_dep],
  link_with : [libhybris_common, libhardware],
  version : '1.0.0',
  install : true
)

subdir('platforms')
