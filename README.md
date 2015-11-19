# Netbeans in a container

All credits goes to [Fabio Rehm](https://github.com/fgrehm) for his [repo](https://github.com/fgrehm/docker-netbeans) for this image.

For the way to run graphical app within docker you should check the [post](https://blog.jessfraz.com/post/docker-containers-on-the-desktop/) from Jessie Frazelle, along with her [dockerfiles repo](https://github.com/jfrazelle/dockerfiles).

To run this image do the following:
#### If you are on Linux
```
docker run -ti --rm \
    -e DISPLAY=$DISPLAY \
    -v $HOME/dotfiles/.netbeans-docker:/root/.netbeans \
    -v $(pwd):/workspace \
    --volumes-from maven_data \
    --name netbeans \
    dirichlet/netbeans
```

#### If you are on Mac
You will need [xQuartz](http://www.xquartz.org) installed on your computer.
First use socat (got this from the following [issue](https://github.com/docker/docker/issues/8710) on the docker repository)
```
socat TCP-LISTEN:6000,reuseaddr,fork UNIX-CLIENT:\"$DISPLAY\"
```

Then you can do:
```
docker run -ti --rm \
    -e DISPLAY=192.168.99.1:0 \
    -v $HOME/dotfiles/.netbeans-docker:/root/.netbeans \
    -v $(pwd):/workspace \
    --volumes-from maven_data \
    --name netbeans \
    dirichlet/netbeans
```

This image will use the current directory as the workspace
