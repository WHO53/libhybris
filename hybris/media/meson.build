media_c_args = []
if get_option('trace')
  media_c_args += '-DDEBUG'
endif

libmedia = shared_library('media',
  'media.c',
  c_args : media_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libmedia,
  name : 'libmedia',
  description : 'libmedia',
  version : meson.project_version()
)