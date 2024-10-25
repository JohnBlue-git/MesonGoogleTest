# Find threads
threads_dep = dependency('threads')

# Find GoogleTest
# method 1
cmake = import('cmake')
gtest_proj = cmake.subproject('googletest', required: true)
if gtest_proj.found()
    gtest_dep = declare_dependency(
        dependencies: [
            threads_dep,
            gtest_proj.dependency('gtest'),
            gtest_proj.dependency('gtest_main'),
        ]
    )
    gmock_dep = declare_dependency(
        dependencies: [
            gtest_proj.dependency('gmock')
        ]
    )
else
    assert(
        not get_option('tests').enabled(),
        'Googletest is required if tests are enabled'
    )
endif
# method 2
# !!! though want to use:
# !!! '''
# !!! gtest_dep = dependency('gtest', required = false)
# !!! if not gtest_dep.found()
# !!!   then ...
# !!! '''
# !!! but found out that the dependency() for cmake project will be incorrect;
# !!!                        declare_dependency() is better 

# Set variables
tests_src = [
  'my_test.cpp',
  src_dir / 'caculate.cpp'
]

# Add the test executable
test_exe = executable('my_test', tests_src,
  include_directories : [inc_dir],
  dependencies : [
    gtest_dep,
    gmock_dep],
  install : true, install_dir : bin_dir
)

# Add a test
test('gtest tests', test_exe)
