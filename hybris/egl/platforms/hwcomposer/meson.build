hwc_inc = [hybris_inc,
    platform_common_inc,
    egl_inc,
    egl_platform_common_inc,
    android_inc
]

hwc_link_with = [libhybris_platformcommon, libhybris_eglplatformcommon, libgralloc]

if (ver_major > 4) or (ver_major == 4 and ver_minor >= 2)
    hwc_link_with += libsync
endif

libhybris_hwcomposerwindow = shared_library('hybris-hwcomposerwindow',
  'hwcomposer_window.cpp',
  include_directories : hwc_inc,
  dependencies : [android_headers_dep],
  link_with : hwc_link_with,
  version : '1.0.0',
  install : true
)

pkg.generate(libhybris_hwcomposerwindow,
  name : 'hwcomposer-egl',
  description : 'hwcomposer-egl',
  version : meson.project_version()
)

install_headers('hwcomposer_window.h', 'hwcomposer.h', subdir : 'hybris/hwcomposerwindow')

shared_module('eglplatform_hwcomposer',
  'eglplatform_hwcomposer.cpp',
  include_directories : hwc_inc,
  dependencies : [android_headers_dep],
  link_with : [libhybris_hwcomposerwindow, libhybris_eglplatformcommon, libgralloc],
  name_prefix : '',
  install : true,
  install_dir : join_paths(get_option('libdir'), 'libhybris')
)
