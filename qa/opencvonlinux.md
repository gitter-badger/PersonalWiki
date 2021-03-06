## How to build up OpenCV in Linux [Back](./qa.md)

- **Ubuntu 14.04** + **OpenCV 3.1.0**

#### 1. be sure to install cmake

`sudo apt-get install cmake`

#### 2. download and extract opencv

`wget -O opencv-3.1.0.zip https://github.com/Itseez/opencv/archive/3.1.0.zip`

`upzip opencv-3.1.0.zip`

#### 3. build

##### 3.1 create a build directory

`mkdir build && cd build`

##### 3.2 use cmake to build

`cmake -D WITH_FFMPEG=ON -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON ..`

- Problem: **qmake: could not exec '/usr/lib/i386-linux-gnu/qt4/bin/qmake': No such file or directory**
- Solution: install the `qt` dependence (`sudo apt-get install qt4-qmake libqt4-dev`)
- Problem: **cmake_cxx_compiler not set after enablelanguage**
- Solution: install c++ compiler (`sudo apt-get install g++`)
- Problem:
    - The first "expected" hash should be always same (for specific OpenCV code version).
The second "actual" hash is a signature of received data. And this received data is just broken due some reasons (firewall policy restrictions / other network problems / other software problems, like legacy CMake (2.8.7+ works fine) ): you may try to open file in "mc" editor and check it, sometimes there are messages like "403 forbidden", "timeout", "connection lost".
    - There are some discussion for the similar problem here (but about ffmpeg): [#5546](https://github.com/Itseez/opencv/issues/5546) [#5895](https://github.com/Itseez/opencv/issues/5895)

- Soluton: 
    - disable this feature (`-DWITH_IPP=OFF`)
    - try to download these files manually and put on the right places. You can get these IPPICV files from [here](https://github.com/Itseez/opencv_3rdparty/tree/ippicv/master_20151201/ippicv) in the RAW mode. Script doesn't re-download file if it has right contents and it is located in the right place.

##### 3.3 make

`sudo make -j2`

- *Note: this will take some time to complete. *
- *Note: without ffmpeg, opencv cannot read a video*
- Problem: **some lib*.so have undefined link to reference LibXML2**
- Solution: you should check the lib when installing ffmpeg. *(eg. enable `libbluray` in ffmpeg will cause problem in ubuntu 14.04 when building opencv)*
- Problem: **/usr/bin/ld: /usr/local/lib/libavcodec.a(avpacket.o): relocation R_X86_64_32 against `.rodata.str1.1' can not be used when making a shared object; recompile with -fPIC**.
- Solution: recompile libx264 with `--enable-pic` and `--enable-shared` because your system is 64-bit Ubuntu. (More [details](./../summary/ffmpeg/ffmpeg.md) about installing ffmpeg on Ubuntu 12.04)
- Problem: **No rule to make target '/usr/lib/x86_64-linux-gnu/libGL.so'**
- Solution: try to re-install libgl with `sudo apt-get install --reinstall libgl1-mesa-dev` 

##### 3.4 make install

`sudo make install`

#### 4. Configure

`sudo sh -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'`

`sudo ldconfig`

#### 5. Reboot the computer

#### 6. Create a project and run it

##### 6.1 Create CMakeLists.txt

`vim CMakeLists.txt`
```
cmake_minimum_required(VERSION 2.8)
project( [projectName] )
find_package( OpenCV REQUIRED )
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "lib/")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "lib/")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "bin/")
add_executable( [projectName] [projectName].cpp )
target_link_libraries( [projectName] ${OpenCV_LIBS} )
```

##### 6.2 Run the project

`cmake .`

`make`

`./[projectName]`

<a href="http://aleen42.github.io/" target="_blank" ><img src="./../pic/tail.gif"></a>
