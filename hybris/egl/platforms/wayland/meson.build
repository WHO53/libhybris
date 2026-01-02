shared_module('eglplatform_wayland',
  'eglplatform_wayland.cpp',
  include_directories : [hybris_inc,
    egl_inc,
    platform_common_inc,
    egl_platform_common_inc,
    wayland_inc,
    android_inc
  ],
  dependencies : [android_headers_dep, wayland_dep, wayland_server_dep],
  link_with : [libhybris_eglplatformcommon, libgralloc],
  name_prefix : '',
  install : true,
  install_dir : join_paths(get_option('libdir'), 'libhybris')
)
