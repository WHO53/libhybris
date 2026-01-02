input_c_args = []
if get_option('trace')
  input_c_args += '-DDEBUG'
endif

libis = shared_library('is',
  'is.c',
  c_args : input_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libis,
  name : 'libis',
  description : 'libis',
  version : meson.project_version()
)