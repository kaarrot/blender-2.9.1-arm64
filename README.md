
# Dependencies

    sudo apt-get install build-essential git subversion cmake libx11-dev libxxf86vm-dev libxcursor-dev libxi-dev libxrandr-dev libxinerama-dev libglew-dev
    sudo apt install libjpeg-dev/bionic
    sudo apt install libmp3lame-dev/bionic
    sudo apt install libjack-dev/bionic
    sudo apt install libopenal-dev/bionic    # to enbale sound in Blender system sounds


    
# Build boost
    
    ./b2 --with-program_options  --with-python --with-filesystem --with-system --with-serialization --with regex  --with-locale --prefix=$HOME/toolchains/boost1.71.0 install

# Build Embree (Aarch64)
    https://github.com/lighttransport/embree-aarch64.git
   
    cmake ..   -DEMBREE_ARM=On -DEMBREE_ISPC_SUPPORT=Off -DEMBREE_TASKING_SYSTEM=Internal -DEMBREE_TUTORIALS=Off -DEMBREE_MAX_ISA=SSE2 -DEMBREE_RAY_PACKETS=Off  -DCMAKE_INSTALL_PREFIX=~/toolchains/embree3

# Build ffmpeg (no Neon)

'ffmpeg' folder is picked up by Blender CMake

    ./configure --prefix=$HOME/toolchains/ffmpeg --disable-neon --enable-demuxer=mov,m4v,matroska --enable-muxer=mp3,mp4 --enable-libmp3lame

    make -j 4 install
        
# Build Blender

    cmake .. -DWITH_PYTHON=1 -DPYTHON_VERSION=3.7 -DPYTHON_ROOT_DIR=/home/kuba/toolchains/python37/ -DEMBREE_EMBREE3_LIBRARY=/home/kuba/toolchains/embree3/lib/libembree3.so.3 -DEMBREE_INCLUDE_DIR=/home/kuba/toolchains/embree3/include -DWITH_POTRACE=OFF -DWITH_OPENIMAGEDENOISE=OFF -DWITH_JACK=ON -DWITH_MOD_OCEANSIM=OFF -DBOOST_ROOT=~/toolchains/boost1.71.0/ -DBOOST_INCLUDEDIR=~/toolchains/boost1.71.0/include -DBOOST_LIBRARYDIR=~/toolchains/boost1.71.0/lib -DBoost_NO_SYSTEM_PATHS=ON -DWITH_CYCLES=OFF -DWITH_TBB=OFF -DWITH_INTERNATIONAL=OFF -DCMAKE_INSTALL_PREFIX=install_dir -DCMAKE_BUILD_TYPE=Release
  
    make -j 4 install
