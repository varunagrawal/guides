## CPP Version Change

Below we show an example to downgrade the version of gcc/g++ on one's machine. 
This also serves as an example of changing the version of gcc/g++.

```shell
# Install the version of GCC/G++ using your package manager
sudo apt-get install gcc-4.9 g++-4.9 gcc-4.9-aarch64-linux-gnu      

# get the current GCC version. We shall refer to this as gcc-x
gcc --version

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 100 
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-x 50

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-x 50
```

## Boost

Download and compile Boost from source

```sh
# cd to Boost directory
./bootstrap
./b2
sudo ./b2 install
```

#### Python Config

You might want to configure the python interpreter being used, especially if you use Anaconda Python.

Update the `project-config.jam` file and look for the section

```
# Python configuration
import python ;
if ! [ python.configured ]
{
    using python : 3.7 ;
}
```

Update the line inside the parenthesis to

```
using python : 3.7 : <location of anaconda dir> ;
```

And finally, make sure to link the Boost.Python .so file correctly so programs like CMake can find it correctly. Be sure to replace the correct `libboost_python*.so` file in the command below.

```sh
# .so files
sudo ln -s /use/local/lib/libboost_python37.so.1.67.0 /use/local/lib/libboost_python.so 
sudo ln -s /use/local/lib/libboost_python37.so.1.67.0 /use/local/lib/libboost_python-py3.so

# header
sudo ln -s /usr/local/include/boost/python.hpp /usr/local/include/boost/python-py3.hpp 
```

**NOTE** If you get a conflict when creating the above symlinks (due to pre-existing python2 files), simply rename the python2 files by appending a `-py2` before the file extension and try again.