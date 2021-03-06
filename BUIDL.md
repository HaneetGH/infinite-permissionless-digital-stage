You can create an Infinite Permissionless Digital Stage by running the following commands:

OPEN NEW TERMINAL WINDOW
```
sudo apt install ffmpeg
wget https://github.com/livepeer/go-livepeer/releases/download/v0.5.1/livepeer-linux-amd64.tar.gz
tar -xzf livepeer-linux-amd64.tar.gz
./livepeer-linux-amd64/livepeer -orchestrator -cliAddr 127.0.0.1:7936 -httpAddr 127.0.0.1:8936 -serviceAddr 127.0.0.1:8936 -orchSecret secret -v 99
```
OPEN NEW TERMINAL WINDOW
```
./livepeer-linux-amd64/livepeer -transcoder -cliAddr 127.0.0.1:7937 -httpAddr 127.0.0.1:8937 -orchAddr 127.0.0.1:8936 -orchSecret secret -v 99
```
OPEN NEW TERMINAL WINDOW
```
./livepeer-linux-amd64/livepeer -broadcaster -cliAddr 127.0.0.1:7935 -rtmpAddr 127.0.0.1:1935 -httpAddr 127.0.0.1:8935 -orchAddr 127.0.0.1:8936 -transcodingOptions P144p30fps16x9 -v 99
```
OPEN NEW TERMINAL WINDOW
```
ffmpeg -re -f lavfi -i testsrc=size=426x240:rate=30,format=yuv420p -f lavfi -i sine -threads 1 -c:v libx264 -b:v 10000k -preset ultrafast -x264-params keyint=30 -c:a aac -f flv rtmp://127.0.0.1:1935/hello_world
```
OPEN NEW TERMINAL WINDOW
```
ffplay http://127.0.0.1:8935/stream/hello_world/P144p30fps16x9.m3u8
```
If successful, you should see a test card like this:

![image](https://user-images.githubusercontent.com/59374467/71633051-3a74fb80-2c12-11ea-82d7-d646022216fb.png)
