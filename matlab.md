# Matlab

## Installing MatConvNet

Update GCC to point to the correct compiler version:

```shell
sudo apt-get install gcc-4.9 g++-4.9 gcc-4.9-aarch64-linux-gnu      

# get the current GCC version. We shall refer to this as gcc-x
gcc --version

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 100 
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-x 50

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-x 50
```

You may need to run this to load the libraries correctly.
```
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libstdc++.so.6:/usr/lib/x86_64-linux-gnu/libprotobuf.so.9
```

Install the dependencies, specifically `libjpeg`.
```shell
# If using Ubuntu
sudo apt-get install libjpeg-turbo8-dev
```

Compile 
```matlab
cuda_dir = '/usr/local/cuda-8.0'  % update the directory as required.
vl_compilenn('enableImreadJpeg', true, 'enableGpu', true, 'cudaRoot', [cuda_dir], 'cudaMethod', 'nvcc');
```

If the regular compilation throws issues (especially on CPU only installs), then run this from the Matconvnet directory in the command line. Adjust your MATLAB path accordingly.

```
make ARCH=glnxa64 MATLABROOT=/usr/local/MATLAB/R2017b VERB=yes DEBUG=yes
```

To undo gcc settings:

```
sudo update-alternatives /usr/bin/gcc gcc /usr/bin/gcc-4.9 50 
sudo update-alternatives /usr/bin/gcc gcc /usr/bin/gcc-x 100

sudo update-alternatives /usr/bin/g++ g++ /usr/bin/g++-4.9 50
sudo update-alternatives /usr/bin/g++ g++ /usr/bin/g++-x 100
```
