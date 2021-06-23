<!-- PROJECT LOGO -->
<br />
<p align="center">
  <!--  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a> -->

  <h3 align="center">MMCore, OpenCV, Imgui</h3>

  <p align="center">
    A minimal reproducible example using MMCore to handle microscope I/O, <br>OpenCV for image processing and<br> Imgui for bloat-free GUI with minimal dependencies.
  </p>
</p>


<!-- ABOUT THE PROJECT -->
### About The Project

<img src="https://github.com/tractatus/MMCore_OpenCV_Imgui/blob/main/mmcore_opencv_imgui.gif" width="800"/>


I still havent completely made the compilation of MMCore entirely into CMake so just download the orignal micromanager source code and compile it through their `automake` instructions.

### Installation

Step 1-3 follows the compilation advice for MicroManager Java which compiles MMDevice and makes makefile for MMCore.
After compiling take the entire folder `mmCoreAndDevices` and place in this directory. See:
https://github.com/micro-manager/micro-manager/blob/efb524723a90ed1a329b4423c698edfde59d0629/doc/how-to-build.md

1. Install MicroManager from binary as usual and check that it works with your microscope.
   Then Clone the MicroManager repo:
   ```sh
   git clone https://github.com/micro-manager/micro-manager.git
   ```
2. First check that you have the following dependencies for compiling micromanager:
   ```sh
   which autoconf
   which automake
   which glibtool
   which pkg-config
   brew info boost
   brew info opencv4
   ```
   If not install with homebrew. Boost is necessary for micromanager, opencv is not but this C++ repo uses OpenCV to process the image.
3. Generate configure file:
   ```sh
   ./autogen.sh
   ```
4. Run configure
   ```sh
   ./configure
   ```
5. Compile
   ```sh
   make
   ```
6. Move to `mmCoreAndDevices/MMCore` and make sure it is compiled
   ```sh
   cd ./mmCoreAndDevices/MMCore
   make
   cd ../..
   ```

7. Clone this repo and copy the `mmCoreAndDevices` directory and replace it:
   ```sh
   git clone https://github.com/tractatus/MMCore_OpenCV_Imgui.git
   cp -r ./mmCoreAndDevices ./MMCore_OpenCV_Imgui/
   ```

8. Compile:
   ```sh
   cd MMCore_OpenCV_Imgui
   cmake .
   make
   ```

9. Run:
   ```sh
   ./micromanager
   ```   
