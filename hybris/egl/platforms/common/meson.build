eglplatformcommon_sources = files('eglplatformcommon.cpp')
eglplatformcommon_deps = [android_headers_dep]
eglplatformcommon_link_with = [libhybris_common, libgralloc, libhybris_platformcommon]
eglplatformcommon_c_args = []
eglplatformcommon_cpp_args = []

if (ver_major > 4) or (ver_major == 4 and ver_minor >= 2)
    eglplatformcommon_link_with += libsync
endif

if conf_data.get('WANT_WAYLAND', 0) == 1
  eglplatformcommon_deps += [wayland_dep, wayland_server_dep]
endif

if get_option('mesa')
  eglplatformcommon_c_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
  eglplatformcommon_cpp_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif

if get_option('trace')
  eglplatformcommon_c_args += '-DDEBUG'
  eglplatformcommon_cpp_args += '-DDEBUG'
endif

libhybris_eglplatformcommon = shared_library('hybris-eglplatformcommon',
  eglplatformcommon_sources,
  c_args : eglplatformcommon_c_args,
  cpp_args : eglplatformcommon_cpp_args,
  include_directories : [hybris_inc,
    egl_inc,
    platform_common_inc,
    android_inc],
  dependencies : eglplatformcommon_deps,
  link_with : eglplatformcommon_link_with,
  version : '1.0.0',
  install : true
)

libhybris_eglplatformcommon_dep = declare_dependency(
  link_with : libhybris_eglplatformcommon,
  include_directories : include_directories('.')
)

pkg.generate(libhybris_eglplatformcommon,
  name : 'hybris-egl-platform',
  description : 'hybris-egl-platform',
  version : meson.project_version()
)

install_headers('eglplatformcommon.h', 'eglnativewindowbase.h', 'hybris_nativebufferext.h', subdir : 'hybris/eglplatformcommon')