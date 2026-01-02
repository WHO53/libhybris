executable('getprop', 'getprop.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libandroid_properties,
  install : true
)

executable('setprop', 'setprop.c',
  include_directories : [hybris_inc],
  link_with : libandroid_properties,
  install : true
)