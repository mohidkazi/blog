## Installing CMake on Linux

Installing CMake on linux is really easy, you can find the tutorials everywhere on internet.
You can download Cmake from [release!](https://github.com/Kitware/CMake/releases) or using package manager like apt (_for ubuntu_), Ill recomment building CMake from source, But there are some problems you can face while building cmake from source.

### 1. Download CMake Source
Get the latest  version from github release page.
```shell
~$ cd ~/Downloads
~/Downloads$ wget https://github.com/Kitware/CMake/releases/download/v3.17.1/cmake-3.17.1.tar.gz

```

### 2. Extract Source from tar file
use tar command to extract source code.

`~/Downloads$ tar -zxvf cmake-3.17.1.tar.gz`

then move into the extracted folder.

`~/Downloads$ cd cmake-3.17.1/`

### 3. Configure CMake before Building (Optional)
This step is optional and only do this if you know what you are doing ,unlike me.

enter the command to check all the available options.

`~/Downloads/cmake-3.17.1$ ./configure --help`

### 4. Build Cmake
Enter following command to check available arguments you can pass while building.

`~/Downloads/cmake-3.17.1$ ./bootstrap --help`

This is where we will build Cmake from source.

```shell
~/Downloads/cmake-3.17.1$ ./bootstrap
~/Downloads/cmake-3.17.1$ make
~/Downloads/cmake-3.17.1$ sudo make install
```

### 5. Verify Installation
Run following command to check if CMake is installed properly or not.

`$ cmake --version`

### Issues while building from Source
1. One of the issue that i faced was OPENSSL issue, because buiding CMake natively using [official installation protocol!]() does not have SSL support.
