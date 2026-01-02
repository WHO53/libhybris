vibrator_c_args = []
if get_option('trace')
  vibrator_c_args += '-DDEBUG'
endif

libvibrator = shared_library('vibrator',
  'vibrator.c',
  c_args : vibrator_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libvibrator,
  name : 'libvibrator',
  description : 'libvibrator',
  version : meson.project_version()
)