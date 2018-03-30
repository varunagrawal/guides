# Matlab

## Installing MatConvNet

Update GCC to point to the correct compiler version:

```shell
sudo apt-get install gcc-4.9 g++-4.9          

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 100 
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 50

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 100
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 50
```

You may need to run this to load the libraries correctly.
```
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libstdc++.so.6:/usr/lib/x86_64-linux-gnu/libprotobuf.so.9
```

Compile 
```matlab
cuda_dir = '/usr/local/cuda-8.0'  % update the directory as required.
vl_compilenn('enableImreadJpeg', true, 'enableGpu', true, 'cudaRoot', [cuda_dir], 'cudaMethod', 'nvcc');
```

To undo gcc settings:

```
sudo update-alternatives /usr/bin/gcc gcc /usr/bin/gcc-4.9 50 
sudo update-alternatives /usr/bin/gcc gcc /usr/bin/gcc-5 100

sudo update-alternatives /usr/bin/g++ g++ /usr/bin/g++-4.9 50
sudo update-alternatives /usr/bin/g++ g++ /usr/bin/g++-5 100
```
