
To build the image:
```
docker build --progress=plain -t sawyer-melodic .

```

To run the image + use display + open multiple terminal:

```
xhost + # only have to do once

docker run -it --net=host --env="DISPLAY" --env="QT_X11_NO_MITSHM=1" --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw"  --volume="${PWD}/overlay_ws":"/root/catkin_ws/src/overlay_ws/":rw  sawyer-melodic bash
```

To use ./intera.sh, 

you need to change 'kinetic' to 'melodic'