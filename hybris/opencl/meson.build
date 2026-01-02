opencl_c_args = [
  '-DPKGLIBDIR="@0@"'.format(join_paths(get_option('prefix'), get_option('libdir'), 'libhybris'))
]
if get_option('mesa')
  opencl_c_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif
if get_option('trace')
  opencl_c_args += '-DDEBUG'
endif

if get_option('clicd')
  cl_icd = configure_file(
    input : 'libhybris.icd.in',
    output : 'libhybris.icd',
    configuration : conf_data,
  )

  install_data(
    cl_icd,
    install_dir : join_paths(get_option('sysconfdir'), 'OpenCL', 'vendors')
  )
endif

libopencl = shared_library('OpenCL',
  'opencl.c',
  c_args : opencl_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, dl_dep],
  link_with : libhybris_common,
  version : '1.0.0',
  install : true
)

pkg.generate(libopencl,
  name : 'OpenCL',
  description : 'OpenCL',
  version : meson.project_version()
)
