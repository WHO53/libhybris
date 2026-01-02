test_common_src = files('test_common.cpp')

test_cpp_args = ['-std=gnu++11']
if get_option('mesa')
  test_cpp_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif
if has_hwc2
  test_cpp_args += '-DHAS_HWCOMPOSER2_HEADERS=1'
else
  test_cpp_args += '-DHAS_HWCOMPOSER2_HEADERS=0'
endif

if get_option('glvnd')
  libegl_for_test = dependency('egl')
  libglesv2_for_test = dependency('glesv2')
else
  libegl_for_test = declare_dependency(link_with : libegl)
  libglesv2_for_test = declare_dependency(link_with : libglesv2)
endif

executable('test_audio',
  'test_audio.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libhardware],
  install : true
)

executable('test_egl',
  'test_egl.cpp',
  cpp_args : test_cpp_args,
  include_directories : [hybris_inc, platform_common_inc, egl_platform_common_inc, hwcomposer_inc, libsync_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test],
  link_with : [libhybris_common],
  install : true
)

executable('test_egl_configs',
  'test_egl_configs.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test],
  link_with : [libhybris_common],
  install : true
)

executable('test_glesv2',
  ['test_glesv2.cpp', test_common_src],
  cpp_args : test_cpp_args + ['-DUSE_HWCOMPOSER=1'],
  include_directories : [hybris_inc, platform_common_inc, egl_platform_common_inc, hwcomposer_inc, libsync_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test],
  link_with : [libhybris_common, libhybris_hwcomposerwindow, libhybris_platformcommon, libhybris_eglplatformcommon, libhardware, libsync] + (has_hwc2 ? [libhwc2] : []),
  install : true
)

executable('test_glesv3',
  ['test_glesv3.cpp', test_common_src],
  cpp_args : test_cpp_args + ['-DUSE_HWCOMPOSER=1'],
  include_directories : [hybris_inc, platform_common_inc, egl_platform_common_inc, hwcomposer_inc, libsync_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test],
  link_with : [libhybris_common, libhybris_hwcomposerwindow, libhybris_platformcommon, libhybris_eglplatformcommon, libhardware, libsync] + (has_hwc2 ? [libhwc2] : []),
  install : true
)

test_hwcomposer_link_with = [libhybris_common, libhybris_platformcommon, libhybris_eglplatformcommon, libhardware]
if has_hwc2
  test_hwcomposer_link_with += libhwc2
endif
if ver_major >= 5 or (ver_major == 4 and ver_minor >= 2)
  test_hwcomposer_link_with += [libsync, libhybris_hwcomposerwindow]
endif

executable('test_hwcomposer',
  ['test_hwcomposer.cpp', test_common_src],
  cpp_args : test_cpp_args + ['-DUSE_HWCOMPOSER=1'],
  include_directories : [hybris_inc, platform_common_inc, egl_platform_common_inc, hwcomposer_inc, libsync_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test],
  link_with : test_hwcomposer_link_with,
  install : true
)

executable('test_sensors',
  'test_sensors.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libhardware],
  install : true
)

executable('test_lights',
  'test_lights.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libhardware],
  install : true
)

executable('test_ui',
  'test_ui.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libui],
  install : true
)

executable('test_sf',
  ['test_sf.cpp', test_common_src],
  cpp_args : test_cpp_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test],
  link_with : [libhybris_common, libsf],
  install : true
)

executable('test_input',
  'test_input.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libis],
  install : true
)

executable('test_media',
  ['test_media.cpp', test_common_src],
  cpp_args : test_cpp_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test],
  link_with : [libhybris_common, libmedia, libsf],
  install : true
)

executable('test_recorder',
  ['test_recorder.cpp', test_common_src],
  cpp_args : test_cpp_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test],
  link_with : [libhybris_common, libmedia, libcamera, libis, libsf],
  install : true
)

executable('test_gps',
  'test_gps.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, thread_dep],
  link_with : [libhybris_common, libhardware],
  install : true
)

test_nfc_c_args = []
if has_libnfc
  test_nfc_c_args += '-DHAS_LIBNFC_NXP_HEADERS=1'
else
  test_nfc_c_args += '-DHAS_LIBNFC_NXP_HEADERS=0'
endif

executable('test_nfc',
  'test_nfc.c',
  c_args : test_nfc_c_args + ['-Wno-error=unused-function'],
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep, thread_dep],
  link_with : [libhybris_common, libnfc_nxp, libhardware],
  install : true
)

test_vibrator_c_args = []
if has_vibrator
  test_vibrator_c_args += '-DHAS_VIBRATOR_HEADER=1'
else
  test_vibrator_c_args += '-DHAS_VIBRATOR_HEADER=0'
endif

executable('test_vibrator',
  'test_vibrator.c',
  c_args : test_vibrator_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libhardware, libvibrator],
  install : true
)

test_wifi_c_args = []
if has_wifi
  test_wifi_c_args += '-DHAS_WIFI_LEGACY_HEADERS=1'
else
  test_wifi_c_args += '-DHAS_WIFI_LEGACY_HEADERS=0'
endif

executable('test_wifi',
  'test_wifi.c',
  c_args : test_wifi_c_args,
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libwifi],
  install : true
)

executable('test_opencl',
  'test_opencl.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libopencl],
  install : true
)

executable('test_dlopen',
  'test_dlopen.c',
  include_directories : [hybris_inc, android_inc],
  dependencies : [android_headers_dep],
  link_with : [libhybris_common, libhardware],
  install : true
)

if conf_data.get('WANT_WAYLAND', 0) == 1
  executable('test_camera',
    ['test_camera.cpp', test_common_src],
    cpp_args : test_cpp_args,
    include_directories : [hybris_inc, platform_common_inc, egl_platform_common_inc, hwcomposer_inc, libsync_inc, android_inc],
    dependencies : [android_headers_dep, libegl_for_test, libglesv2_for_test, wayland_dep, wayland_egl_dep],
    link_with : [libhybris_common, libcamera, libis],
    install : true
  )

  if has_vulkan_headers
    executable('test_vulkan',
      'test_vulkan.cpp',
      cpp_args : test_cpp_args,
      include_directories : [hybris_inc, android_inc],
      dependencies : [android_headers_dep, wayland_dep],
      link_with : [libhybris_common, libvulkan],
      install : true
    )
  endif
endif
