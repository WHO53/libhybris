vulkan_wayland_sources = files(
  'vulkanplatform_wayland.cpp',
  'wayland_window.cpp',
  '../../../../platforms/wayland/wayland_window_common.cpp'
)

vulkan_wayland_args = []
if not get_option('wayland_serverside_buffers')
  vulkan_wayland_args += '-DHYBRIS_NO_SERVER_SIDE_BUFFERS'
endif

shared_module('vulkanplatform_wayland',
  vulkan_wayland_sources,
  cpp_args : vulkan_wayland_args,
  include_directories : [hybris_inc, 
    platform_common_inc,
    wayland_inc,
    vulkan_inc,
    vulkan_platform_common_inc,
    android_inc
  ],
  dependencies : [android_headers_dep, wayland_dep, wayland_egl_dep],
  link_with : [libhybris_platformcommon, libhybris_vulkanplatformcommon, libgralloc],
  install : true,
  install_dir : join_paths(get_option('libdir'), 'libhybris')
)
