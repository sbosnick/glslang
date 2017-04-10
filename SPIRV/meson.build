sources = [ 'GlslangToSpv.cpp',
            'InReadableOrder.cpp',
            'Logger.cpp',
            'SpvBuilder.cpp',
            'doc.cpp',
            'disassemble.cpp']

spvremap_sources = ['SPVRemapper.cpp', 'doc.cpp']

headers = [ 'bitutils.h',
            'spirv.hpp',
            'GLSL.std.450.h',
            'GLSL.ext.KHR.h',
            'GlslangToSpv.h',
            'hex_float.h',
            'Logger.h',
            'SpvBuilder.h',
            'spvIR.h',
            'doc.h',
            'disassemble.h']

spvremap_headers = ['SPVRemapper.h', 'doc.h']

if enable_amd_extensions
    headers += 'GLSL.ext.AMD.h'
endif

if enable_nv_extensions
  headers += 'GLSL.ext.NV.h'
endif

SPIRV_lib = static_library('SPIRV', sources, headers,
                link_with: glslang_lib,
                install: true)

SPVRemapper_lib = static_library('SPVRemapper', spvremap_sources, spvremap_headers,
                install: true)

install_headers(headers, spvremap_headers, subdir: 'SPIRV')
