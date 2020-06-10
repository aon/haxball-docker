# Haxball headless server with Docker
This is a simple container that runs [haxroomie-cli](https://github.com/morko/haxroomie) and starts as many rooms as you want given the appropriate config.js file. It's based on Alpine, so it's as lightweight as possible, and it's multi-arch, supporting amd64 and arm64.

# Usage
First you'll need to generate a haxball token https://www.haxball.com/headlesstoken.

Then, make your own `config.js` file and put it on an appropriate folder. We will share this folder with our container. You can find an example in https://github.com/morko/haxroomie/tree/master/packages/haxroomie-cli or in examples/config.js in this repo.

Start the docker container:

```
docker pull aon22/haxball:latest

docker run \
    --name=haxroomie \
    --network host \
    -v /path/to/config:/config \
    aon22/haxball
```

## Using docker-compose
If you want to use docker-compose instead of running and recalling each time every docker command, create a simple `docker-compose.yml` file and fill it.

```
version: '3.4'

services:
  haxroomie:
    image: aon22/haxball
    network: "host"
    volumes:
    - /path/to/config:/config
    stdin_open: true
    tty: true
```

And then run it on the same folder as the file you just created with

```docker-compose up-d```

Remember to make a new token each time you run it and put it `config.js`, otherwise it will not run.

# Todo
- Get it to autobuild from Docker Hub with multiarch
- Build for rpi armv7 (can't use Alpine since there isn't chromium support for arm 32-bit)
