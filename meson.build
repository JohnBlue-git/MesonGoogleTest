project('MyProject', 'cpp', 
  default_options : ['cpp_std=c++14']
)

# Set include directory
inc_dir = include_directories('include')

# Set source directory
src_dir = meson.current_source_dir() / 'source'

# Set customized bin directory
bin_dir = meson.current_source_dir() / 'bin'

# Add the src directory
subdir('source')

# Add the tests directory
subdir('tests')
