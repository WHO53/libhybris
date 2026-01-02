ui_c_args = []
if get_option('trace')
  ui_c_args += '-DDEBUG'
endif

libui = shared_library('ui',
  'ui.c',
  c_args : ui_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

libui_dep = declare_dependency(link_with : libui)