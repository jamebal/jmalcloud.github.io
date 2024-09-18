# 部署后无法查看office文档

假设网盘地址为: http://localhost:7070, 则office地址为: http://localhost:7071/office/

外层nginx需要加上`proxy_set_header Host $http_host;`
```nginx
location ^~ / {
    proxy_pass http://localhost:7070; 
    proxy_set_header Host $http_host; 
    proxy_set_header X-Real-IP $remote_addr; 
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
    proxy_set_header REMOTE-HOST $remote_addr; 
    proxy_set_header Upgrade $http_upgrade; 
    proxy_set_header Connection $http_connection; 
    proxy_set_header X-Forwarded-Proto $scheme; 
    proxy_http_version 1.1; 
    add_header X-Cache $upstream_cache_status; 
    add_header Cache-Control no-cache; 
    proxy_ssl_server_name off; 
    add_header Strict-Transport-Security "max-age=31536000"; 
}
```
