Dante - A free SOCKS server
===========================

**the original project - [vimagick/dante][1]** and it has its own [automatic build on dockerhub][2]. 

[Dante][3] is a product developed by Inferno Nettverk A/S. It consists of a
SOCKS server and a SOCKS client, implementing RFC 1928 and related standards.
It is a flexible product that can be used to provide convenient and secure
network connectivity. 

**changes:**
- debian stretch-slim instead of jessie
- required username authentication
- fix dante package checksum

## docker-compose

```
dante:
  image: djhumster/dante-srv
  ports:
    - "1080:1080"
  volumes:
    - ./sockd.conf:/etc/sockd.conf
  restart: until-stopped
```

## up and running

```
$ docker-compose up -d
# or
$ docker run -d -p 1080:1080 --restart unless-stopped --name dante djhumster/dante-srv

# Required username authentication.
$ docker exec -it dante_dante_1 bash
>>> useradd -M -N -s /bin/false username
>>> passwd username
>>> exit

$ curl -x socks5://username:password@127.0.0.1:1080 https://ya.ru
```

[1]: https://github.com/vimagick/dockerfiles/tree/master/dante
[2]: https://hub.docker.com/r/vimagick/dante/
[3]: http://www.inet.no/dante/index.html

## sockd.conf

```
debug: 0
logoutput: stderr

internal: 0.0.0.0 port = 1080
external: eth0
 
clientmethod: none
socksmethod: username

user.privileged: root
user.unprivileged: nobody

# allow any client connection
client pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    log: error
}

# deny proxied to lo
socks block {
    from: 0.0.0.0/0 to: 127.0.0.0/8
    log: error
}

# deny binding
socks block {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    command: bind
    log: error
}

socks pass {
    from: 0.0.0.0/0 to: 0.0.0.0/0
    socksmethod: username
    log: error
}
```
