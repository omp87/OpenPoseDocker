# OpenPose Dockerfile

This project creates a Docker image for OpenPose project

## Building Container
```
docker build -f Dockerfile.cpu -t openpose:cpu .
```


## Running Container
Running this container is made complex because OpenPose by default creates a graphical window. This cause the application to terminate this. We handle this by installing a dummy display driver, but this requires a startup script that starts the display to a dummy screen using Xfvb and then ultimately calling OpenPose. To do these both tasks in a way that is dynamic, we put the command we want to run in command.sh. The Entrypoint command copies this command into /entrypoint.sh and then calls /entrypoint.sh. This means a user needs to mount the command.sh file. See the sample run command

```
docker run -it -v $(pwd)/command.sh:/command.sh -v $(pwd)/output_jsons:/output_jsons  -v $(pwd)/output_images:/output_images --rm openpose:cpu
```
with the command.sh content
```
./build/examples/openpose/openpose.bin --video examples/media/video.avi --write_json /output_jsons/ --write_images /output_images/
```


A sample example to analyze images in a directory
```
docker run -it -v $(pwd)/command.sh:/command.sh -v $(pwd)/samples:/samples -v $(pwd)/output_jsons:/output_jsons  -v $(pwd)/output_images:/output_images --rm openpose:cpu
```

With the command.sh content
```
./build/examples/openpose/openpose.bin --image_dir /samples/ --write_json /output_jsons/ --write_images /output_images/
```