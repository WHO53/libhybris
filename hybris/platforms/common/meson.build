platformcommon_sources = files(
  'nativewindowbase.cpp',
  'platformcommon.cpp',
  'windowbuffer.cpp'
)

platformcommon_c_args = []
platformcommon_cpp_args = []
platformcommon_deps = [android_headers_dep]
platformcommon_link_with = [libhybris_common, libgralloc]

if (ver_major > 4) or (ver_major == 4 and ver_minor >= 2)
    platformcommon_link_with += libsync
endif

if conf_data.get('WANT_WAYLAND', 0) == 1
  platformcommon_sources += files(
    'server_wlegl.cpp',
    'server_wlegl_handle.cpp',
    'server_wlegl_buffer.cpp'
  )
  
  platformcommon_deps += [wayland_dep, wayland_server_dep]

  wl_gen_c = custom_target('wayland-android-protocol-c',
    input : 'wayland-android.xml',
    output : 'wayland-android-protocol.c',
    command : [wayland_scanner, 'code', '@INPUT@', '@OUTPUT@']
  )
  
  wl_gen_client_h = custom_target('wayland-android-client-protocol-h',
    input : 'wayland-android.xml',
    output : 'wayland-android-client-protocol.h',
    command : [wayland_scanner, 'client-header', '@INPUT@', '@OUTPUT@']
  )
  
  wl_gen_server_h = custom_target('wayland-android-server-protocol-h',
    input : 'wayland-android.xml',
    output : 'wayland-android-server-protocol.h',
    command : [wayland_scanner, 'server-header', '@INPUT@', '@OUTPUT@']
  )
  
  platformcommon_sources += [wl_gen_c, wl_gen_client_h, wl_gen_server_h]
endif

if get_option('mesa')
  platformcommon_c_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
  platformcommon_cpp_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif

if get_option('trace')
  platformcommon_c_args += '-DDEBUG'
  platformcommon_cpp_args += '-DDEBUG'
endif

libhybris_platformcommon = shared_library('hybris-platformcommon',
  platformcommon_sources,
  c_args : platformcommon_c_args,
  cpp_args : platformcommon_cpp_args,
  include_directories : [hybris_inc,
    egl_inc,
    android_inc],
  dependencies : platformcommon_deps,
  link_with : platformcommon_link_with,
  version : '1.0.0',
  install : true
)

libhybris_platformcommon_dep = declare_dependency(
  link_with : libhybris_platformcommon,
  include_directories : platform_common_inc
)

install_headers('support.h', 'nativewindowbase.h', subdir : 'hybris/platformcommon')