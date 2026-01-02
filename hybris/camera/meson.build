camera_c_args = []
if get_option('trace')
  camera_c_args += '-DDEBUG'
endif

libcamera = shared_library('camera',
  'camera.c',
  c_args : camera_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libcamera,
  name : 'libcamera',
  description : 'libcamera',
  version : meson.project_version()
)