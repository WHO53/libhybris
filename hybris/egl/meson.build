egl_sources = files('egl.c', 'helper.cpp', 'ws.c')

egl_c_args = [
  '-DPKGLIBDIR="@0@"'.format(join_paths(get_option('prefix'), get_option('libdir'), 'libhybris')),
  '-DDEFAULT_EGL_PLATFORM="@0@"'.format(get_option('default_egl_platform'))
]
egl_cpp_args = egl_c_args

egl_deps = [android_headers_dep, dl_dep]
egl_link_with = [libhybris_common, libhardware]

if get_option('glvnd')
  egl_sources += files(
    'glvnd/eglglvnd.cpp',
    'glvnd/egldispatchstubs.c'
  )
  
  dispatch_stub_xml = files(
    'glvnd/generate/egl.xml',
    'glvnd/generate/egl_other.xml',
    'glvnd/generate/egl_hybris.xml'
  )
  
  g_egldispatchstubs_h = custom_target('g_egldispatchstubs.h',
    input : dispatch_stub_xml,
    output : 'g_egldispatchstubs.h',
    command : [python3, join_paths(meson.current_source_dir(), 'glvnd/generate/gen_egl_dispatch.py'), 'header', '@INPUT@'],
    capture : true
  )

  g_egldispatchstubs_c = custom_target('g_egldispatchstubs.c',
    input : dispatch_stub_xml,
    output : 'g_egldispatchstubs.c',
    command : [python3, join_paths(meson.current_source_dir(), 'glvnd/generate/gen_egl_dispatch.py'), 'source', '@INPUT@'],
    capture : true
  )
  
  egl_sources += [g_egldispatchstubs_h, g_egldispatchstubs_c]
  
  egl_deps += [libglvnd_dep]
  
  egl_c_args += ['-fvisibility=hidden']
  egl_cpp_args += ['-fvisibility=hidden']
  
  gl_lib_suffix = get_option('glvnd') ? '_libhybris' : ''

  glvnd_conf = configuration_data()
  glvnd_conf.set('GL_LIB_SUFFIX', gl_lib_suffix)
  
  glvnd_json = configure_file(
    input  : 'glvnd/10_libhybris.json.in',
    output : '10_libhybris.json',
    configuration : glvnd_conf,
  )
  
  install_data(
    glvnd_json,
    install_dir : join_paths(get_option('datadir'), 'glvnd', 'egl_vendor.d')
  )
endif

if get_option('mesa')
  egl_c_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
  egl_cpp_args += '-DLIBHYBRIS_WANTS_MESA_X11_HEADERS'
endif

if get_option('trace')
  egl_c_args += '-DDEBUG'
  egl_cpp_args += '-DDEBUG'
endif

egl_inc_dirs = [
      hybris_inc,
      platform_common_inc,
      include_directories('.'),
      android_inc]

if get_option('glvnd')
   egl_inc_dirs += include_directories('glvnd')
endif

libegl = shared_library('EGL' + (get_option('glvnd') ? '_libhybris' : ''),
  egl_sources,
  c_args : egl_c_args,
  cpp_args : egl_cpp_args,
  include_directories : egl_inc_dirs,
  dependencies : egl_deps,
  link_with : egl_link_with,
  version : get_option('glvnd') ? '0.0.0' : '1.0.0',
  install : true
)

if not get_option('glvnd')
  pkg.generate(libegl,
    name : 'egl',
    description : 'egl',
    version : meson.project_version()
  )
endif

install_headers('eglhybris.h', subdir : 'EGL')
install_headers('ws.h', subdir : 'hybris/eglplatformcommon')

subdir('platforms')
