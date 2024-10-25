## Common features / syntax of Meson

### Add subdirectory (sub-project)
```meson
subdir('sub_directory')
```

###Include header
```meson
# Include directory for all targets
inc = include_directories('include_directory')

# Usage in target
executable('app', 'app.cpp', include_directories : inc)
```

### Add executable or library
```meson
# Executable
executable('app', 'app.cpp')

# Static Library
static_library('lib', 'lib.cpp')

# Shared Library
shared_library('libshared', 'libshared.cpp')
```

### Link or load library
In Meson, the distinction between static and shared libraries is made during the target creation.
```meson
# Link libraries to executable or library
executable('app', 'app.cpp', link_with : 'lib')
```

### Add Dependencies
```meson
# Declare dependencies
dep_lib1 = static_library('lib1', 'lib1.cpp')
dep_lib2 = static_library('lib2', 'lib2.cpp')

# Add dependencies
exe = executable('app', 'app.cpp', link_with : [dep_lib1, dep_lib2])
```

### Installation settings
The default installation prefix in Meson is /usr/local. The installation paths for executables and libraries can be customized.
```meson
# Install files
install_data('file.conf', install_dir : join_paths(get_option('datadir'), 'doc'))

# Install header files
install_headers('header.h', subdir : 'include')

# Example for installing executables and libraries
executable('app', 'app.cpp', install : true)

static_library('lib', 'lib.cpp', install : true)

shared_library('libshared', 'libshared.cpp', install : true)
```

And if you need customized install prefix:
```meson
# Set install prefix
meson setup builddir --prefix /desired/install/path

meson install -C builddir
```

However, **Meson** doesn't set install prefixes directly within its script. It’s more of a command-line setup kind of deal when you configure your build directory.

**Meson** also can’t specify custom permissions during the install process like CMake does.
