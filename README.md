### Compiling Arduino IDE with DTR/RTS Patch for using Serial Monitor with ESP8266

Download jdk-8u111-windows-i586.exe from http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html and install with default settings.

Download https://cygwin.com/setup-x86.exe and install adding wget to the default packages.

Enter Cygwin enviroment using the icon from desktop and use the following commands to download necessary tools.

```
wget http://rawgit.com/transcode-open/apt-cyg/master/apt-cyg
install apt-cyg /bin
rm apt-cyg

apt-cyg update
apt-cyg install git make mingw64-i686-gcc-core mingw64-i686-gcc-g++ perl zip unzip patch nano

wget https://www.apache.org/dist/ant/binaries/apache-ant-1.9.7-bin.zip
unzip apache-ant-1.9.7-bin.zip

nano .bash_profile
```

add the following lines at the end of the file (the first two lines is not mandatory)

```
LANG=en_US.UTF-8
alias dir="ls -al --color"

export JAVA_HOME="/cygdrive/c/Program Files (x86)/Java/jdk1.8.0_111"
export ANT_HOME=~/apache-ant-1.9.7
export PATH=~/apache-ant-1.9.7/bin:$PATH
```

At this step you must exit and re-enter Cygwin enviroment for the changes to take effect, or you can manually execute the export lines if you don't want to do so.

Continue with the following commands to download/patch/build the Arduino source.

```
wget https://github.com/arduino/Arduino/archive/1.8.0.zip
mv 1.8.0.zip Arduino-1.8.0.zip
unzip Arduino-1.8.0.zip
cd Arduino-1.8.0

wget https://github.com/arduino/Arduino/pull/4102.patch
mv 4102.patch SerialMonitor.patch
patch -b -p1 < SerialMonitor.patch

cd build
ant dist
```

Press enter when you are asked for a version number to choose the default value and after a long downloading and building process you can find your freshly build arduino-1.8.0-windows.zip file in the following folder:

```
C:\cygwin\home\yourwindowsusername\Arduino-1.8.0\build\windows
```
