# clbp-publication

This repository is made up of a series of submodules. Make sure all submodules are initialised and cloned.
You can use the command ``git submodule update --init --recursive`` to do so after cloning.

## Building the physical robot example
The physical sumo robot implementation consists of two parts: The computer controller (RoboNet) that generated the steering command  and the arduino sketch that controls the robot's servo motors.

The sketch to upload to the Arduino is provided in [[TODO]]

### Building RoboNet
RoboNet has the following dependencies that must be installed:
- ``boost``
- ``opencv``

In order to build:
- enter the RoboNet directory -- ``cd RoboNet``
- create a build directory -- ``mkdir build``
- run cmake -- ``cmake ..``
- run the build system -- ``make``


The tracking executable(``camtrack``) is not built by default, as it requires the opencv's ``tracking`` extra module (see https://github.com/opencv/opencv_contrib).
If the module is installed, and you want to build ``camtrack``, enable the ``BUILD_TRACKING`` option at the cmake invocation:

``cmake -DBUILD_TRACKING=ON ..``


## Building the Enki simulation
The simulation requires both the Enki and clbp libraries to be built first.

## Building Enki
- ``cd enki-1/enki``
- ``mkdir build && cd build``
- ``qmake ..``
- ``make``
- record the path to both the generated library file (``libenki.a``) and of the ``include`` directory.

## Building ClBP
ClBP uses cmake. just enter the clBP directory from the root and type:
- ``mkdir build && cd build``
- ``cmake ..``
- ``make``
- record the path to both the generated library file (``libclBP.a``) and of the ``include`` directory.
## Building line_follower
Once both libraries have been installed, you can build ``line_follower`` through the following steps:
- ``cd enki-1/examples/line_follower/``
- modify the ``playground.pro`` file to add the ``libclBP.a, libenki.a`` dependencies and the associated include directories (eg:
``INCLUDEPATH += /home/user/clbp-publication/enki-1/enki/include/ /home/user/clbp-publication/clBP/include/    
/home/bruno/deleteme/RoboNet/clBP/include  
LIBS    += /home/user/clbp-publication/enki-1/enki/build/libenki.a /home/user/clbp-publication/clBP/build/libclBP.a  
/home/bruno/deleteme/RoboNet/clBP/include``)
- ``mkdir build && cd build``
- ``qmake ..``
- ``make``

