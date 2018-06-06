Dante - A free SOCKS server
===========================

**the original project - [vimagick/dante][1]** and it has its own [automatic build on dockerhub][2]. 

[Dante][3] is a product developed by Inferno Nettverk A/S. It consists of a
SOCKS server and a SOCKS client, implementing RFC 1928 and related standards.
It is a flexible product that can be used to provide convenient and secure
network connectivity. 

## up and running

```
$ docker-compose up -d

# Required username authentication.
$ docker exec -it dante_dante_1 bash
>>> useradd -M -N -s /bin/false username
>>> echo username:password | chpasswd -c SHA256
>>> exit

$ curl -x socks5://username:password@127.0.0.1:1080 https://ya.ru
```

[1]: https://github.com/vimagick/dockerfiles/tree/master/dante
[2]: https://hub.docker.com/r/vimagick/dante/
[3]: http://www.inet.no/dante/index.html
