shared_module('eglplatform_null',
  'eglplatform_null.c',
  include_directories : [hybris_inc,
    egl_inc,
    egl_platform_common_inc,
    android_inc
  ],
  dependencies : [android_headers_dep],
  link_with : [libhybris_eglplatformcommon, libgralloc],
  name_prefix : '',
  install : true,
  install_dir : join_paths(get_option('libdir'), 'libhybris')
)
