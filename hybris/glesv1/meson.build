glesv1_c_args = []
if get_option('mesa')
  glesv1_c_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif

if get_option('trace')
  glesv1_c_args += '-DDEBUG'
endif

libglesv1_cm = shared_library('GLESv1_CM' + (get_option('glvnd') ? '_libhybris' : ''),
  'glesv1_cm.c',
  c_args : glesv1_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.1.0',
  install : true
)

if not get_option('glvnd')
  pkg.generate(libglesv1_cm,
    name : 'glesv1_cm',
    description : 'glesv1_cm',
    version : meson.project_version()
  )
endif