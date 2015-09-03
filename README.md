# todo

- supervisor配置文件(/etc/supervisor/conf.d/todo.ini)

    [program:todo]
    command=/home/ubuntu/.virtualenvs/todo/bin/uwsgi --ini /data/web/todo/uwsgi.ini
    user=www-data
    autostart=true

- nginx配置文件(/etc/nginx/conf.d/todo.conf)

    server {
        server_name todo.renren001.com;

        location / {
            include     uwsgi_params;
            uwsgi_pass  unix:/var/run/www-data/todo.sock;

            proxy_redirect     off;
            proxy_set_header   Host $host;
            proxy_set_header   X-Real-IP $remote_addr;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Host $server_name;
        }
    }
