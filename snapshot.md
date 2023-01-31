# Create Snapshoot Tutorial

There is no need to create sub-domain. You can use your domain default configuration

This is my configuration:
```bash
My domain : dnsarz.xyz
Main website is : http://dnsarz.xyz
Default web folder (NGINX) : /var/www/html
Default Nginx Configuration : /etc/nginx/sites-enabled/default
```

## Create Directory for snapshot

```bash
mkdir -p /var/www/html/snapshot/planq/
```
## Installation Package

```bash
sudo apt install lz4
cd $HOME/.planqd
sudo systemctl stop planqd
tar -cf - data | lz4 > mkdir -p /var/www/html/snapshot/planq/planq-snapshot-$(date +%Y%m%d).tar.lz4
sudo systemctl start planqd
```

edit `/etc/nginx/sites-enabled/default` and add this line
![image](https://user-images.githubusercontent.com/16186519/215653837-795b5ea2-467b-476f-b231-5b7d8178b5c4.png)

```bash
        location /snapshot/planq {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                autoindex on;
                autoindex_exact_size off;
                autoindex_format html;
                autoindex_localtime on;
        }
```


## Restart Web Server

```bash
service nginx restart

```

## Check your snapshot
```
http://your_domain/snapshot/planq/ 
```
![image](https://user-images.githubusercontent.com/16186519/215654319-5c840516-6b64-4f55-aec3-55be8afa21e5.png)