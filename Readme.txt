cross-compile

sudo apt-get update

sudo apt-get upgrade


----------


sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3 libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libboost-all-dev libboost-program-options-dev

sudo apt-get install libminiupnpc-dev libzmq3-dev libgmp3-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler libqrencode-dev unzip doxygen cmake nsis wine-stable wine64 bc

----------

Install BLS signatures.

cd ~/

wget https://github.com/codablock/bls-signatures/archive/v20181101.zip

unzip v20181101.zip

cd bls-signatures-20181101

cmake .

sudo make install

----------

Build a 32-bit wallet


sudo apt install g++-mingw-w64-i686 mingw-w64-i686-dev

Set the default i686-w64-mingw32-gcc and i686-w64-mingw32-g++ compiler option to posix.

sudo update-alternatives --set i686-w64-mingw32-gcc /usr/bin/i686-w64-mingw32-gcc-posix

sudo update-alternatives --set i686-w64-mingw32-g++ /usr/bin/i686-w64-mingw32-g++-posix

----------

Build i686-w64-mingw32-g++.

PATH=$(echo "$PATH" | sed -e 's/:\/mnt.*//g')

cd depends


----------

The following command will take +/- 30 minutes to complete.

make -j6 HOST=i686-w64-mingw32

cd ..

Execute the following commands to compile the wallet.

./autogen.sh

CONFIG_SITE=$PWD/depends/i686-w64-mingw32/share/config.site ./configure --prefix=/

make -j6


----------

******* Build a 64-bit wallet *******


----------
sudo apt install g++-mingw-w64-x86-64

Set the default x86_64-w64-mingw32-g++ compiler option to posix.

sudo update-alternatives --config x86_64-w64-mingw32-g++

----------
Build x86_64-w64-mingw32-g++.


PATH=$(echo "$PATH" | sed -e 's/:\/mnt.*//g')

cd depends


----------

make -j8 HOST=x86_64-w64-mingw32

cd ..

----------

./autogen.sh

CONFIG_SITE=$PWD/depends/x86_64-w64-mingw32/share/config.site ./configure --prefix=/

make -j6



--------------------------------------

LINUX 

NEW DASH COMpiled

sudo -s

apt-get update

apt-get install -y curl build-essential libtool autotools-dev automake pkg-config python3 bsdmainutils cmake

wget https://github.com/codablock/bls-signatures/archive/v20181101.zip

unzip v20181101.zip

cd bls-signatures-20181101

cmake .

make install

cd ..

git clone https://github.com/dashpay/dash

cd dash/depends

make -j30

cd ..

./autogen.sh

./configure --with-gui=no --prefix=$(pwd)/depends/x86_64-pc-linux-gnu

make -j8
