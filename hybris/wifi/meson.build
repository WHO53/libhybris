wifi_c_args = []
if get_option('trace')
  wifi_c_args += '-DDEBUG'
endif

libwifi = shared_library('wifi',
  'wifi.c',
  c_args : wifi_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libwifi,
  name : 'libwifi',
  description : 'libwifi',
  version : meson.project_version()
)