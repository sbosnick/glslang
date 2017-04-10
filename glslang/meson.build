if host_system == 'windows'
  subdir('OSDependent/Windows')
elif host_system == 'linux' or host_system == 'darwin'
  subdir('OSDependent/Unix')
else
  message('unknown platform')
endif

sources = [ #'MachineIndependent/glslang.y',
            'MachineIndependent/glslang_tab.cpp',
            'MachineIndependent/Constant.cpp',
            'MachineIndependent/iomapper.cpp',
            'MachineIndependent/InfoSink.cpp',
            'MachineIndependent/Initialize.cpp',
            'MachineIndependent/IntermTraverse.cpp',
            'MachineIndependent/Intermediate.cpp',
            'MachineIndependent/ParseContextBase.cpp',
            'MachineIndependent/ParseHelper.cpp',
            'MachineIndependent/PoolAlloc.cpp',
            'MachineIndependent/RemoveTree.cpp',
            'MachineIndependent/Scan.cpp',
            'MachineIndependent/ShaderLang.cpp',
            'MachineIndependent/SymbolTable.cpp',
            'MachineIndependent/Versions.cpp',
            'MachineIndependent/intermOut.cpp',
            'MachineIndependent/limits.cpp',
            'MachineIndependent/linkValidate.cpp',
            'MachineIndependent/parseConst.cpp',
            'MachineIndependent/reflection.cpp',
            'MachineIndependent/preprocessor/Pp.cpp',
            'MachineIndependent/preprocessor/PpAtom.cpp',
            'MachineIndependent/preprocessor/PpContext.cpp',
            'MachineIndependent/preprocessor/PpMemory.cpp',
            'MachineIndependent/preprocessor/PpScanner.cpp',
            'MachineIndependent/preprocessor/PpSymbols.cpp',
            'MachineIndependent/preprocessor/PpTokens.cpp',
            'MachineIndependent/propagateNoContraction.cpp',
            'GenericCodeGen/CodeGen.cpp',
            'GenericCodeGen/Link.cpp']

glslang_public_headers = [ 'Public/ShaderLang.h' ]
glslang_general_headers = [
            'Include/arrays.h',
            'Include/BaseTypes.h',
            'Include/Common.h',
            'Include/ConstantUnion.h',
            'Include/InfoSink.h',
            'Include/InitializeGlobals.h',
            'Include/intermediate.h',
            'Include/PoolAlloc.h',
            'Include/ResourceLimits.h',
            'Include/revision.h',
            'Include/ShHandle.h',
            'Include/Types.h']
glslang_mach_indep_headers = [
            'MachineIndependent/glslang_tab.cpp.h',
            'MachineIndependent/gl_types.h',
            'MachineIndependent/Initialize.h',
            'MachineIndependent/iomapper.h',
            'MachineIndependent/LiveTraverser.h',
            'MachineIndependent/localintermediate.h',
            'MachineIndependent/ParseHelper.h',
            'MachineIndependent/reflection.h',
            'MachineIndependent/RemoveTree.h',
            'MachineIndependent/Scan.h',
            'MachineIndependent/ScanContext.h',
            'MachineIndependent/SymbolTable.h',
            'MachineIndependent/Versions.h',
            'MachineIndependent/parseVersions.h',
            'MachineIndependent/propagateNoContraction.h']
glslang_mach_indep_pp_headers = [
            'MachineIndependent/preprocessor/PpContext.h',
            'MachineIndependent/preprocessor/PpTokens.h']
headers = [glslang_public_headers, glslang_general_headers,
           glslang_mach_indep_headers, glslang_mach_indep_pp_headers]

glslang_link_with = [ OGLCompiler_lib, OSDependent_lib]
if enable_hlsl
    glslang_link_with += HLSL_lib
endif

glslang_lib = static_library('glslang', sources, headers,
                link_with: glslang_link_with,
                install: true)

install_headers(glslang_public_headers, subdir:host_path_seperator.join(['glslang', 'Public']))
install_headers(glslang_general_headers, subdir:host_path_seperator.join(['glslang', 'Include']))
install_headers(glslang_mach_indep_headers, subdir:host_path_seperator.join(['glslang', 'MachineIndependent']))
install_headers(glslang_mach_indep_pp_headers,
                subdir:host_path_seperator.join(['glslang', 'MachineIndependent', 'preprocessor']))
