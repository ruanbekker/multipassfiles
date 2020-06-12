Launch an instance:

```
$ multipass launch bionic \
  --name go-dev \
  --cpus 1 \
  --mem 512m \
  --disk 1G \
  --cloud-init cloud-init.yml
```

Exec into your instance and test go:

```
$ multipass exec go-dev bash
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@go-dev:~$ go version
go version go1.14.4 linux/amd64

ubuntu@go-dev:~$ go get github.com/ruanbekker/drone-with-go
ubuntu@go-dev:~$ drone-with-go
hello, world
```
