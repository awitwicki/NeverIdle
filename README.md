# NeverIdle

*Forked from [layou233/NeverIdle](https://github.com/layou233/NeverIdle) and [M3chD09](https://github.com/M3chD09/NeverIdle) (docker support)*

<span style="color:red">**Oracle Cloud Cleaning Up Idle Compute Instances & How to Keep it**</span> (based on this [article](https://blog.51sec.org/2023/02/oracle-cloud-cleaning-up-idle-compute.html))

This program is casually written, and the introduction below is also casually written. If you don't like it, don't touch it.

## One-click script One click to go

```shell
bash <(curl -s -L https://gist.githubusercontent.com/Ansen/e45320205faf5786d3282ac880f20bab/raw/onekey-NeverIdle.sh)
```

MJJ probably likes this. Thanks to script author @Ansen

By default, the following commands are executed, but it is certainly impossible to cover all needs.
For example, AMD does not have 2G memory and does not have the requirement to waste memory.
So it is still recommended that you install it yourself, which is also very convenient and fast.

## Usage

Download the executable file from Release. Note the distinction between amd64 and arm64.

Start a screen on the server, then run this program, search for usage yourself.

Command parameters:

```shell
./NeverIdle -c 2h -m 2 -n 4h
```

Among them:

-c indicates that CPU is periodically wasted, followed by the interval between each waste.
For example, if it is wasted once every 12 hours 23 minutes and 34 seconds, it is 12h23m34s. Fill in according to the format.

-m indicates the amount of memory wasted, followed by a number, in GiB.
After starting, it will occupy the corresponding amount of memory and will not be released until the process is manually killed.

-n indicates that network is periodically wasted, followed by the interval between each waste.
The format is the same as CPU. It will periodically perform an Ookla Speed Test (and output the results!)

-t specifies the number of concurrent connections for periodic network waste.
The default is 10, the higher the value, the more resources consumed, and generally there is no need to change.

*After starting this program, all the functions you configured will be executed immediately, and you can observe the effect. *


## Docker

```shell
docker run ghcr.io/m3chd09/neveridle /app/NeverIdle -c 2h -m 2 -n 4h
```

docker-compose.yml

```yaml
version: '3.9'
services:
  app:
    image: ghcr.io/m3chd09/neveridle
    command: /app/NeverIdle -c 2h -m 2 -n 4h
    restart: always
    volumes:
      - /etc/ssl/certs/ca-certificates.crt:/etc/ssl/certs/ca-certificates.crt:ro
```

## Run this repo in Docker Compose

```shell
git clone https://github.com/awitwicki/NeverIdle.git
cd NeverIdle
docker-compose up -d
```
