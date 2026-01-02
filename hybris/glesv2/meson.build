glesv2_c_args = []
if get_option('mesa')
  glesv2_c_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif

if get_option('trace')
  glesv2_c_args += '-DDEBUG'
endif

libglesv2 = shared_library('GLESv2' + (get_option('glvnd') ? '_libhybris' : ''),
  'glesv2.c',
  c_args : glesv2_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '2.0.0',
  install : true
)

if not get_option('glvnd')
  pkg.generate(libglesv2,
    name : 'glesv2',
    description : 'glesv2',
    version : meson.project_version()
  )
endif