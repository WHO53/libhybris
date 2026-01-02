shared_module('eglplatform_fbdev',
  files('eglplatform_fbdev.cpp', 'fbdev_window.cpp'),
  include_directories : [hybris_inc,
    egl_inc,
    platform_common_inc,
    egl_platform_common_inc,
    android_inc
  ],
  dependencies : [android_headers_dep],
  link_with : [libhybris_platformcommon, libhybris_eglplatformcommon, libgralloc],
  install : true,
  install_dir : join_paths(get_option('libdir'), 'libhybris')
)