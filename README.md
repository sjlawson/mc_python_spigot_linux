# Setting up minecraft for most recent version with Spigot and python api

## Prerequisites:
Python3.6 or newer with venv module
Java 8 (JRE and JDK - openjdk is great)

## Spigot

download buildtools from:
https://hub.spigotmc.org/jenkins/job/BuildTools/

Build for specific version of MC:
`java -jar BuildTools.jar --rev 1.14.4`

Run server:
`java -Xms512M -Xmx1024M -XX:MaxPermSize=128M -jar spigot-1.14.4.jar`

(you may be required to accept the EULA by editing the text file it tells you about)

After the server has run successfuly, enter a `stop` command

## Get RaspberryJuice
This package is needed to setup the correct API routes for python
Install maven:

`sudo apt install maven`  

Build the raspberry juice package:

```
git clone https://github.com/zhuowei/RaspberryJuice
cd RaspberryJuice
mvn package
```

Copy the produced file to the Spigot plugins directory:
`cp target/raspberryjuice-1.11.jar ~/mc_python/plugins/`

## Setup Python virtual environment and get py3minepi

1. Create a working directory for your python files
2. Get Mac minecraft tools (they say for Mac, but all you need is the python package): https://sourceforge.net/projects/program-with-minecraft-mac/
3. Extract the download and copy the folder, `py3minepi-master` to your working directory
4. in your working directory, create a python virtualenv with:
`python3.7 -m venv py`
5. activate the virtualenv:
`source py/bin/activate`
6. install the py3minepi package:
`pip install ./py3minepi-master`

## Test the installation!

1. start the server:
(you may need to fill in a full path for spigot-n.nn.n.jar)
`java -Xms512M -Xmx1024M -XX:MaxPermSize=128M -jar spigot-1.14.4.jar`
2. start minecraft and login to the localhost minecraft server
  - get somewhere in the game where you wont immediately die.
  - alt-tab out to the terminal
3. With the python virtual environment activated `source py/bin/activate` start a python console session by simply typing  `python`
4. Import and enter a test command:
```
>>> from mcpi.minecraft import Minecraft
>>> mc = Minecraft.create()
>>> mc.player.getTilePos()
Vec3(117,2,-63)
```

It's important to note that this vector is not your absolute position in the world, but your position relative to your spawn point.
