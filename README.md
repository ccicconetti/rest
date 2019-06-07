# uiiit::rest library

A simple wrapper to the C++ REST SDK from Microsoft https://github.com/Microsoft/cpprestsdk.

## Build instructions

First, make sure you have [CMake](https://cmake.org/) (version >= 3.2), a recent C++ compiler and all the dependencies installed:

- [glog](https://github.com/google/glog)
- [Boost](https://www.boost.org/)
- [gRPC](https://grpc.io/)
- [protobuf](https://developers.google.com/protocol-buffers/)

Very likely you can find packaged versions of the first two (glog and Boost) in your system's package repository.
Make sure you are installing the development version of the packages, which also include header files.
gRPC is better built from source, and it may automatically download and compile protobuf too (recommended).

Note that [gmock](https://github.com/google/googlemock) is also needed to compile the unit tests but, if everything goes right, it will be downloaded automatically by CMake (needless to say: you do need a working Internet connection for this step).
Also, the library uses [uiiitsupport](https://github.com/ccicconetti/support/), included as a sub-module.

Once everything is ready (assuming `clang++` is your compiler):

```
cd build/debug
../build.sh clang++
```

This will compile the full build tree consisting of:

1. `Rest`: library with simple wrappers of cpprest
3. `Test`: unit tests, which you can execute with `Test/testmain`

If you want to compile with compiler optimisations and no assertions:

```
cd build/release
../build.sh clang++
```

The unit tests will not be compiled (gmock will not be even downloaded).

## How to use in your code

At least two ways:

1. [recommended] Include the full git source tree in your project as a submodule (e.g., under `rest`), add a `add_subdirectory(rest/Rest)` directive to your `CMakeLists.txt` file, fix the header inclusion path so that is also searches in there, and finally in all your targets that use the library add `uiiitrest`.

2. Copy the header files in your header inclusion path, copy the compiled libraries in your library inclusion path.

Method 1 is preferrable because: the dependency stays together with your code; if improvements/fixes are made to the library you just have to update the submodule.

## List of modules

### uiiit::rest

- `Client`: wrapper of `web::http::client::http_client`
- `Server`: wrapper of `web::http::experimental::listener::http_listener`
- `DataType`: wrapper of `web::json::value`
- `ProblemDetails`: _Problem Details_ object, as defined in [IETF RFC 7807](https://tools.ietf.org/html/rfc7807)
