# nginx
### include 
```
server {
        listen       8383;
        server_name  localhost;

        charset utf-8;

        location / {
                root   /home/ubuntu/dist;
                index  index.html index.htm;
        }
}
```
____
```
server {
        listen       8383;
        server_name  localhost;

        charset utf-8;

        location / {
                root   /static-web/dist;
                index  index.html index.htm;
        }
}
```
