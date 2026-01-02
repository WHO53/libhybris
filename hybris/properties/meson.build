libandroid_properties = shared_library('android-properties',
  'hybris_properties.c',
  include_directories : [hybris_inc],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libandroid_properties,
  name : 'libandroid-properties',
  description : 'libandroid-properties',
  version : meson.project_version()
)