**Version 1.0.1 for public testing**

This release should fix an issue that the client was having if connection was lost to the server.  It also updates to cuda 12.8 in preparation for the Nvidia 50 series GPUS.  I beleiave that the RTX 50 Seriese will be verson 10.0 so I have built for that.

Website https://www.challengepool.net/

This is a modified version of the KeyHunt software that has been modified to work with the pool server.  The server will automatically send work in increments that each take about 60 seconds for your worker to complete.   It may take a few work batches for the server to learn the correct speed for your worker.  

Download the required version for your NVidia GPU.

- [`ccap_61.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_61.tar.gz) - GTX 10 Series - `57ad4f81247ca8f27fea1a74491fac75e08314ad2b01be43f918cf494269401e`
- [`ccap_70.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_70.tar.gz) - TITAN V - `afae956b1f43edccaf3eda1956d99ec918b4542281aff3d2b0b7b0cb1526d905`
- [`ccap_75.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_75.tar.gz) - RTX 20 Series - `daf373090fa47071af1d021ba4650534b375bb401cb543afef82308c1ed7f9a3`
- [`ccap_86.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_86.tar.gz) - RTX 30 Series - `e95b01c3c1a6c83d1c90b27d94db659a5910f36c691e9db9d35efa30d4dfb515`
- [`ccap_89.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_89.tar.gz) - RTX 40 Series - `2338ef0c3543e8d2783ded3c2e7102952bca983e6789d4dd4c67e021d8ebd172`
- [`ccap_90.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_90.tar.gz) - H100/H200 - `200b10042604d114c5ef5b362adfc88083594314ae89e58c8ea1921b120ee0c7`
- [`ccap_100.tar.gz`](https://github.com/jrharp/challengepool.net/releases/download/v1.0.1/ccap_100.tar.gz) - RTX 50 Series - `6eafcf7f566fd426fe8f65f29864069010aa605894bc79e988d76628278cbb4f`


If you would like to run on Docker, I have found that this image will run the program out of the box without the need to install dependencies.

https://hub.docker.com/r/nvidia/cuda/

This has been setup to run on a WSL2 Ubuntu instance, I have been using 22.04.  I currently have no plans to compile for windows.  This will install the dependences for the client software for WSL2, if you have a pure Linux environment you will need to also install the relevant NVIDIA driver and CUDA runtime for your system.  Other required dependences can be found in the install_cuda.sh.

Feel free to join the [Discord](https://discord.gg/ryD8tChjt7) if you are interested.

**Setup Instructions**  

```
sudo chmod +x install_cuda.sh
./install_cuda.sh
```


expand the tar file and change directory to the executable folder.

```
tar -xzf ccap_86.tar.gz
cd ccap_86/bin/
sudo chmod +x KeyHunt 
```

The program should run with the example below, just adjust your payment address -a and worker -w

```
./KeyHunt --gpu -m pool -s btc.challengepool.net -p 8001 -a YOURBITCOINPAYMNETADDRESS -w YOURWOKERNAME
./KeyHunt --gpu -m pool -s btc.challengepool.net -p 8001 -a 37CDsFQ4wN5xjAnuSe5CxvPbk7H2vhH2kv -w 3080

```

If you have multiple GPUs you will need to add the flag --gpui with your GPUs IDs 

```
./KeyHunt --gpu --gpui 0,1,2,3,4,5,6,7 -m pool -s btc.challengepool.net -p 8001 -a YOURBITCOINPAYMNETADDRESS -w YOURWOKERNAME
./KeyHunt --gpu --gpui 0,1,2,3,4,5,6,7 -m pool -s btc.challengepool.net -p 8001 -a 37CDsFQ4wN5xjAnuSe5CxvPbk7H2vhH2kv -w 4090

```

The worker program will start and display an update after each work assignment is received by the worker.

- [Puzzle: 67] - Current puzzle
- [Shares: 8522.00 ] - The number of shares the worker has completed
- [EST Payment: 0.841207 BTC] - The current estimated payment for the worker if the solution was found by the pool now
- [Searched: 0.000944 %] - The current percentage of the puzzle hex range that has been searched by the pool

```
KeyHunt-Cuda v1.0 Pool Mode

COMP MODE    : COMPRESSED
COIN TYPE    : BITCOIN
SEARCH MODE  : Pool Mode
DEVICE       : GPU
CPU THREAD   : 0
GPU IDS      : 0
GPU GRIDSIZE : -1x128 (Auto grid size)
SSE          : YES
RKEY         : 0 Mkeys
MAX FOUND    : 65536
POOL MODE    : Payment Address: 37CDsFQ4wN5xjAnuSe5CxvPbk7H2vhH2kv, Worker Name: 3080-2
POOL MODE    : Pool Address: btc.challengepool.net, Port: 8001
[Pool] Successfully connected to pool server btc.challengepool.net:8001 using SSL

Start Time   : Sat Dec 28 09:15:31 2024
Global range : 0000000000000000000000000000000000000000000000000000001BF08EAFFF (37 bit)

GPU          : GPU #0 NVIDIA GeForce RTX 3080 (68x128 cores) Grid(544x128)
[00:00:14] [GPU: 2362.51 Mk/s] [C: 27.57 %] [T: 33,084,669,952 (35 bit)] [Puzzle: 67] [Shares: 8522.00 ] [EST Payment: 0.841207 BTC] [Searched: 0.000944 %]
```



