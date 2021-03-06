# TH++: installation

TH++ requires a Linux x86_64 system with a recent version of gcc (4.8+) that
supports C++11. We confirmed this installation procedure on Ubuntu 13.10 and
14.04 LTS, but other recent versions of Linux should work as well with some
changes.

tl;dr - Install [Torch](http://torch.ch/). Then run `THPP_NOFB=1 build.sh`. For
full functionality, also install [folly](https://github.com/facebook/folly) and
[fbthrift](https://github.com/facebook/fbthrift), and instead run `build.sh`.

1. Install [Torch](http://torch.ch/). The Torch home page has simple scripts
   to automate installing Torch on Ubuntu. **NOTE** that, even though you might
   already have Torch installed, you should reinstall, as older versions do not
   install LuaJIT with Lua 5.2 compatibility. To check, run
   `luajit -e ';;'` -- if you get an error ("unexpected symbol near ';'"),
   then you need to reinstall.
2. **(optional)** Install [folly](https://github.com/facebook/folly). The folly
   [README](https://github.com/facebook/folly/blob/master/README) lists the
   packages (all from the standard Ubuntu distribution) that you need installed
   on your system before compiling folly.
3. **(optional)** Install [fbthrift](https://github.com/facebook/fbthrift). 
   fbthrift depends on folly, and fbthrift's
   [README](https://github.com/facebook/fbthrift/blob/master/README.md) lists
   additional required packages (again, from the standard Ubuntu distribution).
4. Compile and build TH++. This is a standard cmake project; see
   `cd thpp; ./build.sh`, or use cmake directly. If you didn't install folly or 
   fbthrift, you will have to exclude parts that use them from the build. This
   can be achieved with `NO_FOLLY` and `NO_THRIFT` cmake options.
5. Just like most cmake projects, TH++ builds in a separate build directory; if
   anything goes wrong during the build and you want to start over, just delete
   the `build` directory and run `build.sh` again. `THPP_NOFB=1 build.sh`
   installs without folly and thrift. Some functions will be broken, but most
   of the usability is there.
6. Confirm installation; if you used the default installation options, you
   should have `/usr/local/include/thpp/Tensor.h` and
   `/usr/local/lib/libthpp.so`.
