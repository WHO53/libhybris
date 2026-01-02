hwc2_c_args = []
if get_option('trace')
  hwc2_c_args += '-DDEBUG'
endif

if has_hwc2
  hwc2_c_args += '-DHAS_HWCOMPOSER2_HEADERS=1'
else
  hwc2_c_args += '-DHAS_HWCOMPOSER2_HEADERS=0'
endif

libhwc2 = shared_library('hwc2',
  'hwc2.c',
  c_args : hwc2_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libhwc2,
  name : 'libhwc2',
  description : 'libhwc2',
  version : meson.project_version()
)