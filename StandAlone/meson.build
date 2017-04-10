  glslang_default_resource_limits_lib = static_library('glslang_default_resource_limits',
                    'ResourceLimits.cpp',
                    include_directories: root_inc)
  glslang_default_resource_limits_inc = include_directories('.')

  libraries = [glslang_lib, SPIRV_lib, SPVRemapper_lib, glslang_default_resource_limits_lib]

  glslangValidator_exe = executable('glslangValidator', 'StandAlone.cpp',
                    link_args: glslang_link_args,
                    install: true,
                    link_with: libraries,
                    dependencies: thread_dep,
                    include_directories: root_inc)

  spirv_remap_exe = executable('spirv-remap', 'spirv-remap.cpp',
                    link_args: glslang_link_args,
                    install: true,
                    link_with: libraries,
                    dependencies: thread_dep,
                    include_directories: root_inc)
