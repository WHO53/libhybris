nfc_nxp_c_args = []
if has_libnfc
  nfc_nxp_c_args += '-DHAS_LIBNFC_NXP_HEADERS=1'
else
  nfc_nxp_c_args += '-DHAS_LIBNFC_NXP_HEADERS=0'
endif

if get_option('trace')
  nfc_nxp_c_args += '-DDEBUG'
endif

libnfc_nxp = shared_library('nfc_nxp',
  'libnfc_nxp.c',
  c_args : nfc_nxp_c_args + ['-Wno-error=unused-function'],
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libnfc_nxp,
  name : 'libnfc_nxp',
  description : 'libnfc_nxp',
  version : meson.project_version()
)