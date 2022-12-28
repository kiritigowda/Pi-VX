[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

<p align="center"> &nbsp; &nbsp;&nbsp; &nbsp;&nbsp; <img width="10%" src="https://www.raspberrypi.org/app/uploads/2018/03/RPi-Logo-Reg-SCREEN.png" /> &nbsp; &nbsp;&nbsp; &nbsp;&nbsp; <img width="8%" src="https://svgsilh.com/svg/156116.svg"/> &nbsp; &nbsp;&nbsp; &nbsp;&nbsp; <img width="40%" src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/OpenVX_logo.svg/1024px-OpenVX_logo.svg.png?20210508034815"/> </p> 

# Pi-VX
**OpenVX for Raspberry Pi**

<a href="https://www.raspberrypi.org" target="_blank">Raspberry Pi</a> is an ultra low cost computer popular among the DIY developers. It's used in a myriad of commercial and hobbyist projects. <a href="https://www.khronos.org/openvx/" target="_blank">OpenVX™</a> is an open, royalty-free API standard for cross-platform acceleration of computer vision applications developed by <a href="https://www.khronos.org" target="_blank">The Khronos Group</a>. The Khronos Group is an open industry consortium of over 150 leading hardware and software companies creating advanced, royalty-free, acceleration standards for 3D graphics, Augmented and Virtual Reality, vision, and machine learning. Khronos standards include Vulkan®, OpenCL™, SYCL™, OpenVX™, NNEF™, and many others.

Application developers may always freely use Khronos Standards when they are available on the target system. To enable companies to test their products for conformance, Khronos has established an Adopters Program for each standard. This helps to ensure that Khronos standards are consistently implemented by multiple vendors to create a reliable platform for developers. Conformant products also enjoy protection from the Khronos IP Framework, ensuring that Khronos members will not assert their IP essential to the specification against the implementation.

The Khronos Group and the Raspberry Pi Foundation have come together to implement an open-source implementation of <a href="https://www.khronos.org/registry/OpenVX/specs/1.3/html/OpenVX_Specification_1_3.html" target="_blank">OpenVX™ 1.3</a>, which passes the conformance on Raspberry Pi. The open-source implementation passes the Vision, Enhanced Vision, & Neural Net conformance profiles specified in OpenVX 1.3 on Raspberry Pi.

<p align="center"><img width="60%" src="https://www.khronos.org/assets/uploads/apis/2019-openvx-lp-graph.png" /></p> 

OpenVX enables a performance and power-optimized computer vision processing, especially important in embedded and real-time use cases such as face, body, and gesture tracking, smart video surveillance, advanced driver assistance systems (ADAS), object and scene reconstruction, augmented reality, visual inspection, robotics and more. The developers can take advantage of using this robust API in their application and know that the application is portable across all the <a href="https://www.khronos.org/conformance/adopters/conformant-products/openvx" target="_blank">conformant hardware</a>.

<p align="center"><img width="60%" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f1/Raspberry_Pi_4_Model_B_-_Side.jpg/440px-Raspberry_Pi_4_Model_B_-_Side.jpg" /></p> 

In this project, we will go over how to build and install open-source OpenVX 1.3 library on [Raspberry Pi 4 Model B Rev 1.2](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/). We will run the conformance for the Vision, Enhanced Vision, & Neural Net conformance profiles and create a simple computer vision application to get started with OpenVX on Raspberry Pi.

## OpenVX 1.3 Implementation for Raspberry Pi

The [OpenVX 1.3 implementation](https://github.com/KhronosGroup/OpenVX-sample-impl/tree/openvx_1.3) is available on GitHub. To build and install the library follow the instructions below.

### Build OpenVX 1.3 on Raspberry Pi

* Git Clone project with the recursive flag to get submodules.

````
git clone --recursive https://github.com/KhronosGroup/OpenVX-sample-impl.git
````
**Note:** The API Documents and Conformance Test Suite are set as submodules in the sample implementation project 

* Use Build.py script to build and install OpenVX 1.3

````
cd OpenVX-sample-impl/
python Build.py --os=Linux --venum --conf=Debug --conf_vision --enh_vision --conf_nn
````

* Build and run the conformance

````
export OPENVX_DIR=$(pwd)/install/Linux/x32/Debug
export VX_TEST_DATA_PATH=$(pwd)/cts/test_data/
mkdir build-cts
cd build-cts
cmake -DOPENVX_INCLUDES=$OPENVX_DIR/include -DOPENVX_LIBRARIES=$OPENVX_DIR/bin/libopenvx.so\;$OPENVX_DIR/bin/libvxu.so\;pthread\;dl\;m\;rt -DOPENVX_CONFORMANCE_VISION=ON -DOPENVX_USE_ENHANCED_VISION=ON -DOPENVX_CONFORMANCE_NEURAL_NETWORKS=ON ../cts/
cmake --build .
LD_LIBRARY_PATH=./lib ./bin/vx_test_conformance
````

## Sample Application

Use the open-source [samples](https://github.com/KhronosGroup/openvx-samples) on GitHub to test the installation.

<p align="center"><img width="60%" src="https://github.com/KhronosGroup/openvx-samples/blob/master/images/vx-pop-app.gif?raw=true" /></p> 

#### Acknowledgement

* Raspberry Pi is a trademark of the Raspberry Pi Foundation
* Images used in this document are used for educational purpose
* OpenVX is a trademark of the Khronos Group
