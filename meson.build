project('glslang', 'cpp', default_options: ['cpp_std=c++11'])

enable_amd_extensions = get_option('ENABLE_AMD_EXTENSIONS')
enable_glslang_binaries = get_option('ENABLE_GLSLANG_BINARIES')
enable_nv_extensions = get_option('ENABLE_NV_EXTENSIONS')
enable_hlsl = get_option('ENABLE_HLSL')

global_args = []

if enable_amd_extensions
  global_args += '-DAMD_EXTENSIONS'
endif
if enable_nv_extensions
  global_args += '-DNV_EXTENSIONS'
endif
if enable_hlsl
  global_args += '-DENABLE_HLSL'
endif

host_system = host_machine.system()
if host_system == 'windows'
  global_args += '-DGLSLANG_OSINCLUDE_WIN32'
elif host_system == 'linux' or host_system == 'darwin'
  global_args += '-DGLSLANG_OSINCLUDE_UNIX'
endif

cpp_compiler_id = meson.get_compiler('cpp').get_id()
if cpp_compiler_id == 'gcc' or cpp_compiler_id == 'clang'
    global_args += '-Wno-reorder'
endif

add_global_arguments(global_args, language:'cpp')

if host_system == 'windows' and cpp_compiler_id == 'gcc'
    glslang_link_args = ['-static', '-static-libgcc', '-static-libstdc++']
else
    glslang_link_args = []
endif

if host_system == 'windows'
    host_path_seperator = '\\'
else
    host_path_seperator = '/'
endif

gtest_dep = dependency('gtest', required: false)
gmock_dep = dependency('gmock', required: false)
thread_dep = dependency('threads')

root_inc = include_directories('.')

# Dependancies are handled differntly by Meson so we do not need the External subdir.
# subdir('External')

subdir('OGLCompilersDLL')
if enable_hlsl
  subdir('hlsl')
endif
subdir('glslang')
subdir('SPIRV')
if enable_glslang_binaries
  subdir('StandAlone')
endif
subdir('gtests')
