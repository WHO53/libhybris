sf_c_args = []
if get_option('trace')
  sf_c_args += '-DDEBUG'
endif

libsf = shared_library('sf',
  'sf.c',
  c_args : sf_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libsf,
  name : 'libsf',
  description : 'libsf',
  version : meson.project_version()
)