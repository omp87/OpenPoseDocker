# OpenPose Dockerfile

This project creates a Docker image for OpenPose project

## Building Container
```
docker build -f Dockerfile.cpu -t openpose:cpu .
```


## Running Container
With OpenPose.bin, youl will need to use --display 0 to prevent window from being opened

Also, use [exampls] (https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/scripts/CI/run_tests.sh)