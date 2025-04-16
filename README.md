# 以下操作都是在宝塔面板中完成，远程登陆后需要先下载
# 每次重启云服务器，公网ip可能有变化，需要修改反向代理设置
# 后端需要配置对应语言的虚拟环境
# python方法：python3 -m venv venv
# 前端需要转成静态文件
# 创建的反向代理站点配置文件路径：/www/server/panel/vhost/nginx
# 配置反向代理时，前端静态文件的配置方法和后端动态进程配置的方法不同
# 静态：
location / {
        root /www/wwwroot/121.40.138.55/build;
        index index.html;
        try_files $uri $uri/ /index.html;
    }
# 进程：
location /subjects {
        proxy_pass http://localhost:5000;  # 转发到后端服务
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

# 数据库root有自己的密码，要改对应后端数据库配置
