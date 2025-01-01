# challengepool.net
Bitcoin Challenge Pool 

**Version 1.0 for initial public testing**

This is a modified version of the KeyHunt software that has been modified to work with the pool server.  The server will automatically send work in increments that each take about 60 seconds for your worker to complete.   It may take a few work batches for the server to learn the correct speed for your worker.  

Download the required version for your NVidia GPU.

- ccap_61.tar.gz - GTX 10 Series - 1e8172af47ac046ab1639d988c64d7b5970647f3dfdfbc601d47991d51c78b57
- ccap_70.tar.gz - TITAN V          - 89ff2d92be4f82b3d3b79df73afd190860fe1cac5d3cb20f8b586ad5bbc70f88
- ccap_75.tar.gz - RTX 20 Series - 80f04c8e75b277fd5fab6d48fe4aa73ef578c93aa30f238cae22715180edde06
- ccap_86.tar.gz - RTX 30 Series - 947503b14941a8a695e91eac28fa36d3a759ea76addb0c19b84b16c7a822ba48
- ccap_89.tar.gz - RTX 40 Series - fe7bc715e479a9bcef5eaecc6f2215f384d847f99512e8f25cd067cbcab6c3ee

This has been setup to run on a WSL2 Ubuntu instance, I have been using 22.04.  I currently have no plans to compile for windows.  This will install the dependences for the client software for WSL2, if you have a pure Linux environment you will need to also install the relevant NVIDIA driver and CUDA runtime for your system.  Other required dependences can be found in the install_cuda.sh.

Feel free to join the [Discord](https://discord.gg/ryD8tChjt7) if you are interested.

**Setup Instructions**  

```
sudo chmod +x install_cuda.sh
./install_cuda.sh
```


expand the tar file and change directory to the executable folder.

```
tar -xzf ccap_86.tar
cd ccap_86/bin/
sudo chmod +x KeyHunt 
```

The program should run with the example below, just adjust your payment address -a and worker -w

```
./KeyHunt --gpu -m pool -s btc.challengepool.net -p 8001 -a YOURBITCOINPAYMNETADDRESS -w YOURWOKERNAME
./KeyHunt --gpu -m pool -s btc.challengepool.net -p 8001 -a 37CDsFQ4wN5xjAnuSe5CxvPbk7H2vhH2kv -w 3080

```

The worker program will start and display an update after each work assignment is received by the woker.

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



