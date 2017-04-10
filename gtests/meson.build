if gtest_dep.found() and gmock_dep.found()
    gtest_feature_test_code = '''
        #include <string>
        #include <gtest/gtest.h>

        std::string MakeName(::testing::TestParamInfo<const char *> info) {
            return std::string{ info.param };
        }

        class FeatureTest : public ::testing::TestWithParam<const char *> {
        };

        TEST_P(FeatureTest, IsNotNull) {
            EXPECT_STREQ("Good", GetParam());
        }

        INSTANTIATE_TEST_CASE_P(GoodFeature, FeatureTest, ::testing::Values("Good"), MakeName);
        INSTANTIATE_TEST_CASE_P(BadFeature, FeatureTest, ::testing::Values("Good", "Bad"), MakeName);
    '''

    gtest_feature_test_result = meson.get_compiler('cpp').compiles(
        gtest_feature_test_code,
        name: 'gtest_feature_test',
        dependencies: gtest_dep)

    if gtest_feature_test_result

        message('Google Mock and Google Test found - building tests')

        test_sources = [
            # Framework related source files
            'Initializer.h',
            'main.cpp',
            'Settings.cpp',
            'Settings.h',
            'TestFixture.cpp',
            'TestFixture.h',

            # Test related source files
            'AST.FromFile.cpp',
            'BuiltInResource.FromFile.cpp',
            'Config.FromFile.cpp',
            'HexFloat.cpp',
            'Hlsl.FromFile.cpp',
            'Link.FromFile.cpp',
            'Link.FromFile.Vk.cpp',
            'Pp.FromFile.cpp',
            'Spv.FromFile.cpp',

            # -- Remapper tests
            'Remap.FromFile.cpp'
        ]

        test_default_dir = host_path_seperator.join([meson.source_root(), 'Test'])
        test_cpp_args = '-DGLSLANG_TEST_DIRECTORY="@0@"'.format(test_default_dir)

        test_libraries = [ SPVRemapper_lib, glslang_lib, OSDependent_lib, OGLCompiler_lib, glslang_lib,
                           SPIRV_lib, glslang_default_resource_limits_lib]
        if enable_hlsl
            test_libraries += HLSL_lib
        endif

        glslangtests = executable('glslangtests', test_sources,
            install: true,
            link_args: glslang_link_args,
            cpp_args: test_cpp_args,
            link_with: test_libraries,
            dependencies: [gtest_dep, gmock_dep],
            include_directories: root_inc
        )

        test('glslang tests', glslangtests)

    else

        message('Google Test found but required features not present')

    endif

endif
