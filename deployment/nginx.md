# nginx

## 概述
1. 作用: 使用nginx 代理80端口请求到 api的8000端口, 以及后续其他服务端口.
2. 配置文件地址: API代码里边spec.nginx下
3. log文件地址: workspace/nginxlog/:/data/
4. 配置文件需要因地制宜: 将api container在host上的地址, 更新到的配置文件upstream里边.


## 部署

```
1. docker pull nginx 
2. docker run --name nginx -p 80:80 -p 443:443 --restart always -d -v /home/glrh11/workspace/nginxlog/:/data/ -v /home/glrh11/workspace/read-in-life-api.conf:/etc/nginx/conf.d/read-in-life-api.conf:ro -v /etc/letsencrypt/archive/glrh11.com/:/etc/nginx/cert/:ro   nginx
```

## 配置文件实例

```
# my own write in 2017-06-17
upstream read_in_life_api{
      server 192.168.0.4:8000  max_fails=3  fail_timeout=10s;
}

server {
    listen      80;
    server_name www.glrh11.com;
    charset utf-8;
    rewrite ^(.*)$ http://glrh11.com$1 permanent;
}

server {
    listen      80;
    server_name glrh11.com *.glrh11.com;
    
    location = / {
        root /www/read_in_life_web/;
        index index.html;
    }
    location ~ \.(css|js|ico|html|txt) {
        root /www/read_in_life_web/;
        index index.html;
    }

    location /{
        expires -1;
        proxy_set_header Host $host;
        proxy_pass http://read_in_life_api;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        access_log /data/log/nginx/glrh11.com/access_log main;
        error_log /data/log/nginx/glrh11.com/error_log info;
    }
}

server {
    listen 443 ssl;
    listen [::]:443 ssl ipv6only=on;

    ssl_certificate /etc/nginx/cert/fullchain1.pem;
    ssl_certificate_key /etc/nginx/cert/privkey1.pem;
    ssl_trusted_certificate /etc/nginx/cert/chain1.pem;

    server_name glrh11.com;
    
    location = / {
        root /www/read_in_life_web/;
        index index.html;
    }
    location ~ \.(css|js|ico|html|txt) {
        root /www/read_in_life_web/;
        index index.html;
    }   

    location /{
        expires -1;
        proxy_set_header Host $host;
        proxy_pass http://read_in_life_api;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        access_log /data/log/nginx/glrh11.com/access_log main;
        error_log /data/log/nginx/glrh11.com/error_log info;
    }
}
```

## FAQ

1. 提示 `Is not directory`

-v 文件路径写错了

2. 提示/data/下面的日志路径问题

原因是, nginx不会自动建立相关日志文件夹. `mkdir -p nginxlog/log/nginx/glrh11.com/`

3. 提示80端口被占用

+ 使用具有sudo权限的用户, `netstat -anp | grep 80`, 查找占用80端口的pid;

+ kill这个进程 `kill -9 pid`

4. 关于location match "/" 以便显示首页的说明: location = /
