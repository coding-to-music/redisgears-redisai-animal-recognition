# redisgears-redisai-animal-recognition

This demo combines several [Redis](https://redis.io) data structures and [Redis Modules](https://redis.io/topics/modules-intro)
to process a AnimalRecognitionDemostream of images and filter out the images that contain cats.

It uses:

- Redis Streams to capture the input video stream: `all`
- [RedisGears](https://oss.redislabs.com/redisgears/) to process this stream
- [RedisAI](https://oss.redislabs.com/redisai/) to classify the images with MobilenetV2

It forwards the images that contain cats to a stream: `cats`

It uses [RedisAI Integration](https://github.com/RedisGears/RedisGears/blob/master/docs/redisai.md) in RedisGears with asynchronous function so the server is not blocked while RedisGears is triggering an inference session in RedisAI.

# 🚀 Javascript full-stack 🚀

https://github.com/coding-to-music/redisgears-redisai-animal-recognition

https://redisgears-redisai-animal-recognition.vercel.app

From / By https://github.com/RedisGears/AnimalRecognitionDemo

https://oss.redislabs.com/redisgears/

https://oss.redislabs.com/redisai/

https://github.com/RedisGears/RedisGears/blob/master/docs/redisai.md

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/redisgears-redisai-animal-recognition.git
git push -u origin main
```

## Getting error about missing lfs object so can't push to GitHub

```
git push -u origin main
```

Output

```
LFS upload missing objects: (0/1), 0 B | 0 B/s
  (missing) app/models/mobilenet_v2_1.4_224_frozen.pb (111479258f3841c93d0a7a377c976c24e8281077818991931429d2277dd88590)
Enumerating objects: 238, done.
Counting objects: 100% (238/238), done.
Delta compression using up to 2 threads
Compressing objects: 100% (135/135), done.
Writing objects: 100% (238/238), 30.75 MiB | 52.57 MiB/s, done.
Total 238 (delta 93), reused 221 (delta 86)
remote: Resolving deltas: 100% (93/93), done.
remote: error: GH008: Your push referenced at least 1 unknown Git LFS object:
remote:     111479258f3841c93d0a7a377c976c24e8281077818991931429d2277dd88590
remote: Try to push them with 'git lfs push --all'.
To github.com:coding-to-music/redisgears-redisai-animal-recognition.git
 ! [remote rejected] main -> main (pre-receive hook declined)
error: failed to push some refs to 'git@github.com:coding-to-music/redisgears-redisai-animal-recognition.git'
```

## Remove lfs because the file is missing

```
git lfs uninstall
```

Output

```
Hooks for this repository have been removed.
Global Git LFS configuration has been removed.
```

## Needed to delete the reference & file since it is unavailable:

```java
rm app/models/mobilenet_v2_1.4_224_fronzen.pb
```

## download the file and put the full file in app/models

```java

```

## 1. Setup Git LFS on your system. You only have to do this once per repository per machine

```java
git lfs install Git LFS initialized.
```

Output:

```
Updated git hooks.
Git LFS initialized.
```

##  2. Choose the type of files you want to track, for examples all ISO images, with git lfs track:

```java
git lfs track "*.pb"
```

Resulting in .gitattributes being created with the following content:

```
*.pb filter=lfs diff=lfs merge=lfs -text
```

## 3. The above stores this information in gitattributes files, so that file need to be added to the repository:

```java
git add .gitattributes
```
##  4. Commit, push and work with the files normally:

```java
git add .
git commit -m "Add Big File using LFS"
git push

```
## 

```java

```
## 

```java

```

[![license](https://img.shields.io/github/license/RedisGears/AnimalRecognitionDemo.svg)](https://github.com/RedisGears/AnimalRecognitionDemo)
[![Animal Recognition](https://github.com/RedisGears/AnimalRecognitionDemo/actions/workflows/ci-config.yml/badge.svg)](https://github.com/RedisGears/AnimalRecognitionDemo/actions/workflows/ci-config.yml)
[![Forum](https://img.shields.io/badge/Forum-RedisGears-blue)](https://forum.redislabs.com/c/modules/redisgears)
[![Discord](https://img.shields.io/discord/697882427875393627)](https://discord.gg/6yaVTtp)

# AnimalRecognitionDemo

This demo combines several [Redis](https://redis.io) data structures and [Redis Modules](https://redis.io/topics/modules-intro)
to process a AnimalRecognitionDemostream of images and filter out the images that contain cats.

It uses:

- Redis Streams to capture the input video stream: `all`
- [RedisGears](https://oss.redislabs.com/redisgears/) to process this stream
- [RedisAI](https://oss.redislabs.com/redisai/) to classify the images with MobilenetV2

It forwards the images that contain cats to a stream: `cats`

It uses [RedisAI Integration](https://github.com/RedisGears/RedisGears/blob/master/docs/redisai.md) in RedisGears with asynchronous function so the server is not blocked while RedisGears is triggering an inference session in RedisAI.

## Architecture

![Architecture](/architecture.png#gh-light-mode-only)
![Architecture](/architecture_dm.png#gh-dark-mode-only)

## Requirements

Docker and Python 3

## Running the Demo

To run the demo:

```bash
git clone https://github.com/RedisGears/AnimalRecognitionDemo.git
cd AnimalRecognitionDemo
# If you don't have it already, install https://git-lfs.github.com/ (On OSX: brew install git-lfs)
git lfs install && git lfs fetch && git lfs checkout
```

## Install git-lfs on Ubuntu

```java
sudo apt update
sudo apt install git-lfs

```

For running the demo with `make`, run:

```bash
make start
make camera
```

Then open the [UI](README.md#ui) to watch the result streams.

To end the demo, then to stop the containers:

```bash
make stop
```

Run `make help` for a few more options.

For running the demo manually, run:

```bash
docker-compose up
```

If something went wrong, e.g. you skipped installing git-lfs, you need to force docker-compose to rebuild the containers

```bash
docker-compose up --force-recreate --build
```

Open a second terminal for the video capturing:

```bash
pip install -r camera/requirements.txt
python camera/read_camera.py
```

Or run the camera process in test mode (without streaming from your camera):

```bash
ANIMAL=[cat|dog] python camera/read_camera.py --test
```

## UI

- `http://localhost:3000` shows all the captured frames
- `http://localhost:3001` shows only the framse with cats

## Limitations

This demo is designed to be easy to setup, so it relies heavily on docker.
You can get better performance and a higher FPS by runninng this demo outside docker.
To control the FPS, edit the [gear.py](https://github.com/RedisGears/AnimalRecognitionDemo/blob/master/app/gear.py#L53) file.
