gralloc_sources = files('gralloc.c')
gralloc_c_args = []

if has_gralloc1
  gralloc_sources += files('GrallocUsageConversion.cpp')
  gralloc_c_args += '-DHAS_GRALLOC1_HEADER=1'
else
  gralloc_c_args += '-DHAS_GRALLOC1_HEADER=0'
endif

if get_option('trace')
  gralloc_c_args += '-DDEBUG'
endif

libgralloc = shared_library('gralloc',
  gralloc_sources,
  c_args : gralloc_c_args,
  cpp_args : ['-std=gnu++11'],
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhardware, libui, libhybris_common],
  version : '1.0.0',
  install : true
)

pkg.generate(libgralloc,
  name : 'libgralloc',
  description : 'libgralloc',
  version : meson.project_version()
)