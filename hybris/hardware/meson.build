hardware_c_args = []
if get_option('trace')
  hardware_c_args += '-DDEBUG'
endif

libhardware = shared_library('hardware',
  'hardware.c',
  c_args : hardware_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '2.0.0',
  install : true
)

libhardware_dep = declare_dependency(link_with : libhardware)

pkg.generate(libhardware,
  name : 'libhardware',
  description : 'libhardware',
  version : meson.project_version()
)