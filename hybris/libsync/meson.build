libsync_c_args = []
if get_option('trace')
  libsync_c_args += '-DDEBUG'
endif

libsync = shared_library('sync',
  'sync.c',
  c_args : libsync_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  version : '2.0.0',
  install : true
)

pkg.generate(libsync,
  name : 'libsync',
  description : 'libsync',
  version : meson.project_version()
)