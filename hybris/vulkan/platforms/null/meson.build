shared_module('vulkanplatform_null',
  'vulkanplatform_null.c',
  include_directories : [hybris_inc, 
    vulkan_inc,
    vulkan_platform_common_inc,
    android_inc
  ],
  dependencies : [android_headers_dep, wayland_server_dep],
  link_with : [libhybris_vulkanplatformcommon, libgralloc],
  install : true,
  install_dir : join_paths(get_option('libdir'), 'libhybris')
)
