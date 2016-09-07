# Linux Documentation

### 安装OpenSSH
```bash
# ubuntu apt   centos yum
$ sudo apt install ssh
$ sudo /etc/init.d/ssh start
```
### 安装Varnish
```bash
$ sudo apt install varnish
# set /etc/varnish/default.vcl
backend default {
  .host = "127.0.0.1";
  .port = "8080"  # nginx的端口
}

$ service varnish stop
# set /etc/default/varnish (ubuntu)  /etc/sysconfig/varnish (centos)
DAEMON_OPTS="-a :80 ..."

# Debian (v8+) / Ubuntu (v15.04+)
$ cp /lib/systemd/system/varnish.service /etc/systemd/system/
# set /etc/systemd/system/varnish.service
ExecStart=/usr/sbin/varnishd -a :80 ....
$ systemctl /etc/systemd/system/reload varnish.service

$ service varnish start
```
### 安装Nginx
```bash
$ sudo apt install nginx
# set /et/nginx/sites-eabled
server {
  listen 8080 default_server;
  listen [::]:8080 default_server;
  ...
}
```
