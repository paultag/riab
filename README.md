# riab

## create user

```
$ export FQDN=some.fqdn.here
$ sudo adduser minion --system --home=/srv/${FQDN}/
$ sudo addgroup repo
$ sudo usermod -a -G repo minion
$ sudo usermod -a -G repo `whoami`
$ sudo su -s /bin/bash minion
```

## write nginx config

```
$ sudo cat > /etc/nginx/sites-enabled/${FQDN} <<<EOF
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
