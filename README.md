Performance-wise rest daemon made using libev event loop, able to serve rest status responses at very high speed

## How to build
- sudo apt install libev-dev
- clone this repo
- change folder to the repo root and run make
- run bin/restdaemon
- access server via http://localhost:8888/status

The daemon consumes 10-12Mb of memory even under heavy load and is able to process up to 17000 requests per second, provided there are no bottlenecks in the workers themselves. 

Optionally you can install apache-utils package and access performance results, shown below

## Pmem info under load 50 simultaneous connections using Apache Bench

```
$ pmap $(pgrep restdaemon)
14656:   ./bin/restdaemon
00005569b1256000     24K r-x-- restdaemon
00005569b145b000      4K r---- restdaemon
00005569b145c000      4K rw--- restdaemon
00005569b2293000   2520K rw---   [ anon ]
00007f283c4bf000   1652K r-x-- libm-2.27.so
00007f283c65c000   2044K ----- libm-2.27.so
00007f283c85b000      4K r---- libm-2.27.so
00007f283c85c000      4K rw--- libm-2.27.so
00007f283c85d000   1948K r-x-- libc-2.27.so
00007f283ca44000   2048K ----- libc-2.27.so
00007f283cc44000     16K r---- libc-2.27.so
00007f283cc48000      8K rw--- libc-2.27.so
00007f283cc4a000     16K rw---   [ anon ]
00007f283cc4e000     52K r-x-- libev.so.4.0.0
00007f283cc5b000   2044K ----- libev.so.4.0.0
00007f283ce5a000      4K r---- libev.so.4.0.0
00007f283ce5b000      4K rw--- libev.so.4.0.0
00007f283ce5c000    156K r-x-- ld-2.27.so
00007f283d067000     20K rw---   [ anon ]
00007f283d083000      4K r---- ld-2.27.so
00007f283d084000      4K rw--- ld-2.27.so
00007f283d085000      4K rw---   [ anon ]
00007fffda8d3000    132K rw---   [ stack ]
00007fffda975000     12K r----   [ anon ]
00007fffda978000      4K r-x--   [ anon ]
ffffffffff600000      4K r-x--   [ anon ]
 total            12736K

```


## Performance report made using Apache Bench
```
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)


Server Software:        
Server Hostname:        localhost
Server Port:            9901

Document Path:          /status
Document Length:        Variable

Concurrency Level:      50
Time taken for tests:   5.886 seconds
Complete requests:      100000
Failed requests:        0
Keep-Alive requests:    0
Total transferred:      48000000 bytes
HTML transferred:       35700000 bytes
Requests per second:    16989.89 [#/sec] (mean)
Time per request:       2.943 [ms] (mean)
Time per request:       0.059 [ms] (mean, across all concurrent requests)
Transfer rate:          7964.01 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       3
Processing:     1    3   0.2      3       8
Waiting:        1    3   0.2      3       6
Total:          2    3   0.2      3       9

Percentage of the requests served within a certain time (ms)
  50%      3
  66%      3
  75%      3
  80%      3
  90%      3
  95%      3
  98%      3
  99%      4
 100%      9 (longest request)

```
