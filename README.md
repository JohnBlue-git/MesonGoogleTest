## Common Meson feature / syntax
[common_meson.md](common_meson.md)

## How to build

How to build this project, follow these steps:
```console
# Navigate to the root of your project directory
cd /path/to/my_project

# Meson build
rm rf build && meson setup build

# Navigate to build
cd build

# ninja build
ninja

# Run the tests
ninja test

# Run the app
my_app

# Check dependency
ldd my_test

# Install
ninja install
# or
sudo ninja install
```

Why need sudo ninja install ? \
Because gtest have to be installed in /usr/..., we have to "sudo make install" to let get sufficient permission
```console
-- Installing: /usr/local/include/gtest/internal/custom/gtest.h
-- Installing: /usr/local/include/gtest/internal/custom/gtest-printers.h
-- Installing: /usr/local/include/gtest/gtest-test-part.h
-- Installing: /usr/local/include/gtest/gtest.h
-- Installing: /usr/local/include/gtest/gtest_prod.h
-- Installing: /usr/local/include/gtest/gtest-printers.h
-- Installing: /usr/local/lib/libgtest.a        or   .so
-- Installing: /usr/local/lib/libgtest_main.a   or   .so
-- Installing: /usr/local/lib/pkgconfig/gtest.pc
-- Installing: /usr/local/lib/pkgconfig/gtest_main.pc
-- Installing: /usr/local/lib/cmake/GTest/GTestConfig.cmake
```

When **ninja install**, terminal will prompt out:
```console
Installation failed due to insufficient permissions.
Attempt to use /usr/bin/sudo to gain elevated privileges? [y/n]  
```

## How to install Google Test library

### Method 1: Using Package Manager
```console
# Install Google Test: Install the libgtest-dev package:
sudo apt install libgtest-dev

# Build Google Test Libraries: The libgtest-dev package provides the source code for Google Test, but not the compiled libraries. You'll need to build them manually:
sudo apt install cmake
cd /usr/src/googletest
sudo cmake CMakeLists.txt
sudo make
sudo cp *.a /usr/lib
# -DBUILD_SHARED_LIBS=ON parameter builds GoogleTest libraries as shared libraries. Otherwise, the libraries are built as static libraries.

# Verify Installation: The libraries should now be installed in /usr/lib. You can verify that they are there:
ls /usr/lib | grep gtest
```

### Method 2: Building from Source
```console
# Install Dependencies: Ensure you have the necessary tools for building from source:
sudo apt update
sudo apt install cmake g++ git

# Clone Google Test Repository: Clone the Google Test repository from GitHub
git clone https://github.com/google/googletest.git
cd googletest

# Build and Install Google Test: Create a build directory, compile, and install Google Test:
mkdir build
cd build
cmake ..
make
sudo make install
# -DBUILD_SHARED_LIBS=ON parameter builds GoogleTest libraries as shared libraries. Otherwise, the libraries are built as static libraries.

# Verify Installation: Check if Google Test libraries are in the system:
ls /usr/local/lib | grep gtest
```

### Method 3: Fetch from subprojects director
The command to setup
```console
# setup
meson setup

# setup and build
meson setup build
```
The googletest.wrap file
```console
[wrap-git]
url = https://github.com/google/googletest
revision = HEAD
```
