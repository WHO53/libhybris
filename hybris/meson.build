project('libhybris', ['c', 'cpp'],
  version : '0.1.0',
  default_options : ['warning_level=1', 'c_std=gnu99', 'cpp_std=gnu++11', 'buildtype=debugoptimized'])

cc = meson.get_compiler('c')
cpp = meson.get_compiler('cpp')
pkg = import('pkgconfig')

conf_data = configuration_data()
conf_data.set_quoted('PACKAGE_NAME', meson.project_name())
conf_data.set_quoted('PACKAGE_VERSION', meson.project_version())

add_project_arguments('-D_GNU_SOURCE', language : ['c', 'cpp'])

dl_dep = cc.find_library('dl', required : true)
rt_dep = cc.find_library('rt', required : true)
thread_dep = dependency('threads')

if get_option('experimental')
  conf_data.set('WANT_EXPERIMENTAL', 1)
endif

if get_option('adreno_quirks')
  conf_data.set('WANT_ADRENO_QUIRKS', 1)
endif

if get_option('trace')
  conf_data.set('WANT_TRACE', 1)
  add_project_arguments('-DDEBUG', language : ['c', 'cpp'])
endif

if get_option('arm_tracing')
  conf_data.set('WANT_ARM_TRACING', 1)
endif

if get_option('mesa')
  conf_data.set('WANT_MESA', 1)
endif

if get_option('ubuntu_camera_headers')
  conf_data.set('WANT_UBUNTU_CAMERA_HEADERS', 1)
endif

wayland_dep = dependency('wayland-client', required : get_option('wayland'))
wayland_server_dep = dependency('wayland-server', required : get_option('wayland'))
wayland_egl_dep = dependency('wayland-egl', version : '>= 1.15', required : get_option('wayland'))

if wayland_dep.found() and wayland_server_dep.found() and wayland_egl_dep.found()
  conf_data.set('WANT_WAYLAND', 1)
  
  wayland_scanner = find_program('wayland-scanner', required : get_option('wayland'))
endif

if get_option('glvnd')
  python3 = import('python').find_installation('python3')
  libglvnd_dep = dependency('libglvnd')
  egl_dep = dependency('egl')
  glesv2_dep = dependency('glesv2')
  
  conf_data.set('WANT_GLVND', 1)
  conf_data.set_quoted('GL_LIB_SUFFIX', '_libhybris')
else
  conf_data.set_quoted('GL_LIB_SUFFIX', '')
endif

if get_option('wayland_serverside_buffers')
  conf_data.set('WANT_WL_SERVERSIDE_BUFFERS', 1)
endif

if get_option('property_cache')
  conf_data.set('WANT_RUNTIME_PROPERTY_CACHE', 1)
endif

if get_option('ubuntu_linker_overrides')
  conf_data.set('WANT_UBUNTU_LINKER_OVERRIDES', 1)
endif

arch = get_option('arch')

fs = import('fs')

android_headers_path = get_option('android_headers')
android_headers_dep = []
android_inc = []

if android_headers_path != ''
  
  has_libnfc = fs.exists(join_paths(android_headers_path, 'libnfc-nxp/phLibNfc.h'))
  has_wifi = fs.exists(join_paths(android_headers_path, 'hardware_legacy/wifi.h'))
  has_hwc2 = fs.exists(join_paths(android_headers_path, 'hardware/hwcomposer2.h'))
  has_gralloc1 = fs.exists(join_paths(android_headers_path, 'hardware/gralloc1.h'))
  has_vibrator = fs.exists(join_paths(android_headers_path, 'hardware_legacy/vibrator.h'))

  inc_dirs = [android_headers_path]
  if has_libnfc
    inc_dirs += join_paths(android_headers_path, 'libnfc-nxp')
  endif
  android_inc = include_directories(inc_dirs)
else
  android_headers_dep = dependency('android-headers')
  
  has_gralloc1 = cc.has_header('hardware/gralloc1.h', dependencies : android_headers_dep)
  has_libnfc = cc.has_header('libnfc-nxp/phLibNfc.h', dependencies : android_headers_dep)
  has_wifi = cc.has_header('hardware_legacy/wifi.h', dependencies : android_headers_dep)
  has_hwc2 = cc.has_header('hardware/hwcomposer2.h', dependencies : android_headers_dep)
  has_vibrator = cc.has_header('hardware_legacy/vibrator.h', dependencies : android_headers_dep)
  has_libnfc_nxp = cc.has_header('libnfc-nxp/phLibNfc.h', dependencies: android_headers_dep)

  if has_libnfc and android_headers_dep.type_name() == 'pkgconfig'
    incdir = android_headers_dep.get_variable(pkgconfig : 'includedir', default_value : '')
    if incdir != ''
       possible_libnfc = join_paths(incdir, 'android', 'libnfc-nxp')
       if fs.exists(possible_libnfc)
         android_inc = include_directories(possible_libnfc)
       endif
    endif
  endif
endif

ver_major = -1
ver_minor = -1
ver_patch = -1

check_args = []
if android_headers_path != ''
    foreach d : inc_dirs
        check_args += '-I' + d
    endforeach
else
endif

prefix = '#include <android-version.h>'

if android_headers_path != ''
    ver_major_str = cc.get_define('ANDROID_VERSION_MAJOR', prefix : prefix, include_directories : android_inc)
    ver_minor_str = cc.get_define('ANDROID_VERSION_MINOR', prefix : prefix, include_directories : android_inc)
    ver_patch_str = cc.get_define('ANDROID_VERSION_PATCH', prefix : prefix, include_directories : android_inc)
else
    ver_major_str = cc.get_define('ANDROID_VERSION_MAJOR', prefix : prefix, dependencies : android_headers_dep)
    ver_minor_str = cc.get_define('ANDROID_VERSION_MINOR', prefix : prefix, dependencies : android_headers_dep)
    ver_patch_str = cc.get_define('ANDROID_VERSION_PATCH', prefix : prefix, dependencies : android_headers_dep)
endif

if ver_major_str == ''
    error('Could not detect ANDROID_VERSION_MAJOR')
endif

ver_major = ver_major_str.to_int()
ver_minor = ver_minor_str.to_int()
ver_patch = ver_patch_str.to_int()

message('Android version: @0@.@1@.@2@'.format(ver_major, ver_minor, ver_patch))

conf_data.set('ANDROID_VERSION_MAJOR', ver_major)
conf_data.set('ANDROID_VERSION_MINOR', ver_minor)
conf_data.set('ANDROID_VERSION_PATCH', ver_patch)

default_ld_path = get_option('default_hybris_ld_library_path')
if default_ld_path == ''
  if ver_major >= 7
    if arch == 'arm' or arch == 'x86'
      default_ld_path = '/system/lib:/odm/lib:/vendor/lib'
    else
      default_ld_path = '/system/lib64:/odm/lib64:/vendor/lib64'
    endif
  else
    if arch == 'arm' or arch == 'x86'
      default_ld_path = '/vendor/lib:/system/lib:/odm/lib'
    else
      default_ld_path = '/vendor/lib64:/system/lib64:/odm/lib64'
    endif
  endif
endif
conf_data.set_quoted('DEFAULT_HYBRIS_LD_LIBRARY_PATH', default_ld_path)

conf_data.set_quoted('DEFAULT_EGL_PLATFORM', get_option('default_egl_platform'))

if get_option('mali_quirks')
  conf_data.set('WANT_MALI_QUIRKS', 1)
endif

if get_option('stub_linker')
  conf_data.set('WANT_STUB_LINKER', 1)
endif

configure_file(output : 'config.h', configuration : conf_data)

hybris_inc = include_directories('.', 'include', 'common')
egl_inc = include_directories('egl')
egl_platform_common_inc = include_directories('egl/platforms/common')
vulkan_inc = include_directories('vulkan')
vulkan_platform_common_inc = include_directories('vulkan/platforms/common')
platform_common_inc = include_directories('platforms/common')
wayland_inc = include_directories('platforms/wayland')

subdir('include')
subdir('common')
subdir('properties')
subdir('hardware')
subdir('ui')
subdir('gralloc')

if (ver_major >= 4 and ver_minor >= 2) or ver_major >= 5
    subdir('libsync')
endif

subdir('platforms')
subdir('egl')
subdir('glesv1')
subdir('glesv2')
subdir('sf')
subdir('input')
subdir('camera')
subdir('vibrator')
subdir('media')
subdir('opencl')
subdir('wifi')
subdir('hwc2')

has_vulkan_headers = cc.has_header('vulkan/vulkan.h', dependencies : android_headers_dep, include_directories : android_inc)
if has_vulkan_headers
   subdir('vulkan')
endif

subdir('libnfc_nxp')
subdir('libnfc_ndef_nxp')

subdir('utils')
subdir('tests')
