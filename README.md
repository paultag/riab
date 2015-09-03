# riab

## create user

```
$ export FQDN=some.fqdn.here
$ sudo addgroup repo
$ sudo adduser minion --group repo --system --home=/srv/${FQDN}/
$ sudo usermod -a -G repo `whoami`
$ sudo su -s /bin/bash minion
```

## write nginx config

```
$ sudo tee /etc/nginx/sites-enabled/${FQDN} <<EOF
server {
    listen 80;
    listen [::]:80;
    server_name ${FQDN}

    access_log /srv/${FQDN}/access.log;
    error_log  /srv/${FQDN}/error.log;

    location / {
        alias /srv/${FQDN}/www/;
        autoindex on;
    }
}
EOF
$ sudo service nginx restart
```

## clone tooling

```
% git clone https://github.com/paultag/reprepoman
% echo 'export PATH=${PATH}:${HOME}/reprepoman' >> ${HOME}/.bashrc
```

## create repo

```
% reprepoman infra
```

## install minica

## install deceive

## install minion
