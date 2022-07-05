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

https://github.com/RedisGears/AnimalRecognitionDemo/issues/30

From / By https://github.com/RedisGears/AnimalRecognitionDemo

https://oss.redislabs.com/redisgears/

https://oss.redislabs.com/redisai/

https://github.com/RedisGears/RedisGears/blob/master/docs/redisai.md

https://dev.to/jldec/what-is-git-lfs-28db

https://www.atlassian.com/git/tutorials/git-lfs

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

## download the file from the original repo and put the full file in app/models

```java
# Use this to bring the file here:

rsync -avz -e "ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --progress /home/tmc/ap/cat-detection-video/mobilenet_v2_1.4_224_frozen.pb TomPod:/mnt/volume_nyc1_01/redisgears-redisai-animal-recognition/app/models/
```

## 1. Setup Git LFS on your system. You only have to do this once per repository per machine

From this tutorial: https://dev.to/jldec/what-is-git-lfs-28db

```java
git lfs install Git LFS initialized.
```

Output:

```
Updated git hooks.
Git LFS initialized.
```

## 2. Choose the type of files you want to track, for examples all ISO images, with git lfs track:

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

## 4. Commit, push and work with the files normally:

```java
git add .
git commit -m "Add Big File using LFS"
```

Output:

```
[main e957702] Add Big File using LFS
 3 files changed, 72 insertions(+), 7 deletions(-)
 create mode 100644 .gitattributes
 create mode 100644 app/models/mobilenet_v2_1.4_224_frozen.pb
```

## Push to remote

```java
Enumerating objects: 10, done./1), 24 MB | 0 B/s
Counting objects: 100% (10/10), done.
Delta compression using up to 2 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (7/7), 1.17 KiB | 1.17 MiB/s, done.
Total 7 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To github.com:coding-to-music/redisgears-redisai-animal-recognition.git
   10320c4..e957702  main -> main
```

## Command: git lfs track

```java
git lfs track
```

Output:

```
Listing tracked patterns
    *.pb (.gitattributes)
Listing excluded patterns
```

## Command: git lfs ls-files

```java
git lfs ls-files
```

Output:

```
111479258f * app/models/mobilenet_v2_1.4_224_frozen.pb
```

## make start

```java
make start
```

Output:

```java
Starting redisgears-redisai-animal-recognition_redis_1 ... done
Creating redisgears-redisai-animal-recognition_app_1     ... done
Creating redisgears-redisai-animal-recognition_weball_1  ... done
Creating redisgears-redisai-animal-recognition_webcats_1 ... done
```

## make camera

```java
make camera
```

Output:

```java
python3 camera/read_camera.py
Traceback (most recent call last):
  File "camera/read_camera.py", line 3, in <module>
    import cv2
ModuleNotFoundError: No module named 'cv2'
make: *** [Makefile:39: camera] Error 1
```

## pip3 install opencv-python

```java
pip3 install opencv-python
```

## start redis and other services

```java
docker-compose up
```

## make camera

```java
make camera
```

Output:

```java
python3 camera/read_camera.py
Connected to Redis
Operating in camera mode
[ WARN:0@0.208] global /io/opencv/modules/videoio/src/cap_v4l.cpp (902) open VIDEOIO(V4L2:/dev/video0): can't open camera by index
Traceback (most recent call last):
  File "camera/read_camera.py", line 83, in <module>
    for (count, img) in loader:
  File "camera/read_camera.py", line 35, in __next__
    assert ret_val, 'Webcam Error'
AssertionError: Webcam Error
make: *** [Makefile:39: camera] Error 1
```

## run the camera process in test mode (without streaming from your camera):

```java
ANIMAL=[cat|dog] python camera/read_camera.py --test
```

```java
dog]: command not found
```

## export a value for ANIMAL using quotes

```
export ANIMAL="[cat|dog]"
```

## ensure the value is correct for ANIMAL

```
printenv | grep ANIMAL
```

Output

```
ANIMAL=[cat|dog]
```

## Run the test

```
python camera/read_camera.py --test
```

Output

```
Connected to Redis
Operating in test mode with image [cat|dog].jpg
Traceback (most recent call last):
  File "camera/read_camera.py", line 99, in <module>
    img = cv2.resize(img0, (IMAGE_WIDTH, IMAGE_HEIGHT))
cv2.error: OpenCV(4.4.0) /tmp/pip-req-build-h2062vqd/opencv/modules/imgproc/src/resize.cpp:3929: error: (-215:Assertion failed) !ssize.empty() in function 'resize'
```

## The docker console log shows this (relating to the above test)

```
redis_1    | 1:M 24 Jun 2022 06:42:45.857 * Ready to accept connections
redis_1    | 1:M 24 Jun 2022 06:42:46.795 # <ai> backend TF not loaded, will try loading default backend
redis_1    | 1:M 24 Jun 2022 06:42:46.866 * <ai> TF backend loaded from /usr/lib/redis/modules/backends/redisai_tensorflow/redisai_tensorflow.so
redis_1    | 1:M 24 Jun 2022 06:42:46.887 # <ai> Invalid GraphDef
app_1      | Loading model - Traceback (most recent call last):
app_1      |   File "/app/init.py", line 39, in <module>
app_1      |     res = conn.execute_command('AI.MODELSTORE', 'mobilenet:model', 'TF', 'CPU', 'INPUTS', '1', 'input', 'OUTPUTS', '1', 'MobilenetV2/Predictions/Reshape_1', 'BLOB', model)
app_1      |   File "/usr/local/lib/python3.9/dist-packages/redis/client.py", line 1235, in execute_command
app_1      |     return conn.retry.call_with_retry(
app_1      |   File "/usr/local/lib/python3.9/dist-packages/redis/retry.py", line 46, in call_with_retry
app_1      |     return do()
app_1      |   File "/usr/local/lib/python3.9/dist-packages/redis/client.py", line 1236, in <lambda>
app_1      |     lambda: self._send_command_parse_response(
app_1      |   File "/usr/local/lib/python3.9/dist-packages/redis/client.py", line 1212, in _send_command_parse_response
app_1      |     return self.parse_response(conn, command_name, **options)
app_1      |   File "/usr/local/lib/python3.9/dist-packages/redis/client.py", line 1251, in parse_response
app_1      |     response = connection.read_response()
app_1      |   File "/usr/local/lib/python3.9/dist-packages/redis/connection.py", line 837, in read_response
app_1      |     raise response
app_1      | redis.exceptions.ResponseError: Invalid GraphDef
weball_1   | Redis Labs - app listening on port 3000!
webcats_1  | Redis Labs - app listening on port 3000!
redisgears-redisai-animal-recognition_app_1 exited with code 1
webcats_1  | received: connected
weball_1   | received: connected
```

## make test

```
make test
```

Output:

```
Testing cats ...
cats: FAIL
make: *** [Makefile:24: test] Error 1
```

[![license](https://img.shields.io/github/license/RedisGears/AnimalRecognitionDemo.svg)](https://github.com/RedisGears/AnimalRecognitionDemo)
[![Animal Recognition](https://github.com/RedisGears/AnimalRecognitionDemo/actions/workflows/ci-config.yml/badge.svg)](https://github.com/RedisGears/AnimalRecognitionDemo/actions/workflows/ci-config.yml)
[![Forum](https://img.shields.io/badge/Forum-RedisGears-blue)](https://forum.redislabs.com/c/modules/redisgears)
[![Discord](https://img.shields.io/discord/697882427875393627)](https://discord.gg/6yaVTtp)

# Got feedback from this issue:

https://github.com/RedisGears/AnimalRecognitionDemo/issues/30

Starting with these:

- `export VERBOSE=1`
- `make clean`
- `sudo make setup`
- `make build`

Got this when I ran `make setup`

```
make setup
```

Output:

```
chmod: changing permissions of '/usr/local/bin/docker-compose': Operation not permitted
make: *** [Makefile:43: setup] Error 1
```

Got this when I ran `sudo make setup`

```
sudo make setup
```

Output:

```
Git LFS initialized.
Error: failed to call git rev-parse --git-dir: exit status 128 : fatal: unsafe repository ('/mnt/volume_nyc1_01/redisgears-redisai-animal-recognition' is owned by someone else)
To add an exception for this directory, call:

        git config --global --add safe.directory /mnt/volume_nyc1_01/redisgears-redisai-animal-recognition

Not in a git repository.
```

Ran this, no error messages:

```
git config --global --add safe.directory /mnt/volume_nyc1_01/redisgears-redisai-animal-recognition
```

Ran `make build` and saw no errors

Because I do not have a camera, I will only use the test, not the camera mode:

- `make start` to run docker-compose for Redis in detached mode (don't use for this testing)
- `docker-compose up` to watch the redis log messages

Here is the tail of the logs, most of it looks good, there is lots before this that looks good too:

```
redis_1    | 1:M 05 Jul 2022 21:50:04.257 * <rg> Successfully installed numpy-1.21.6 opencv-python-headless-4.4.0.46
redis_1    |
redis_1    | WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
redis_1    | 1:M 05 Jul 2022 21:50:04.485 * <ai> TF backend loaded from /usr/lib/redis/modules/backends/redisai_tensorflow/redisai_tensorflow.so
redis_1    | 2022-07-05 21:50:04.560832: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
redis_1    | To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
redis_1    | 1:M 05 Jul 2022 21:50:04.804 # <search> Skip background reindex scan, redis version contains loaded event.
redis_1    | 1:M 05 Jul 2022 21:50:04.804 * DB loaded from disk: 10.248 seconds
redis_1    | 1:M 05 Jul 2022 21:50:04.804 * Ready to accept connections
app_1      | Discovered evidence of a previous initialization - skipping.
redisgears-redisai-animal-recognition_app_1 exited with code 0
weball_1   | received: connected
```

Using a different terminal window:

- do not have docker running in the other window, this will be the running process for the test
- `export ANIMAL=cat` or `export ANIMAL=dog`
- `make test` to run the test against the video using either DOG or CAT as our target

```
make clean
make setup
make build
export ANIMAL=dog
make test
```

```
<lots of success messages above>
1657058108889-1  addToGraphRunner: count= 140
1657058108947-0  addToGraphRunner: animal= golden_retriever
1657058108990-0  shouldTakeFrame 141 False
1657058109091-0  shouldTakeFrame 142 False
1657058109192-0  shouldTakeFrame 143 False
1657058109292-0  shouldTakeFrame 144 False
1657058109394-0  shouldTakeFrame 145 False
1657058109494-0  shouldTakeFrame 146 False
1657058109595-0  shouldTakeFrame 147 False
1657058109696-0  shouldTakeFrame 148 False
1657058109797-0  shouldTakeFrame 149 False
1657058109898-0  shouldTakeFrame 150 True
1657058109899-0  addToGraphRunner: count= 150
1657058109956-0  addToGraphRunner: animal= golden_retriever
1657058109999-0  shouldTakeFrame 151 False
1657058110100-0  shouldTakeFrame 152 False
1657058110201-0  shouldTakeFrame 153 False
1657058110302-0  shouldTakeFrame 154 False
1657058110403-0  shouldTakeFrame 155 False
1657058110503-0  shouldTakeFrame 156 False
1657058110604-0  shouldTakeFrame 157 False
Stopping camera.catndogs ... done
Stopping redis.catndogs  ... done
Removing camera.catndogs ... done
Removing app.catndogs    ... done
Removing redis.catndogs  ... done
Removing network catsndogs_default
dogs: OK
```

So, success !!!

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
