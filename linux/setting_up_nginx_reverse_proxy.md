# Setting up nginx reverse proxy

If we have 2 node applications, one for general use (`/`) and one for myservice (`/myservice`), then we need to set a reverse proxy in our nginx server configuration.
```bash
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;
        server_name hellonode;

        location ^~ /assets/ {
                gzip_static on;
                expires 12h;
                add_header Cache-Control public;
        }

        location / {
                proxy_http_version 1.1;
                proxy_cache_bypass $http_upgrade;

                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection 'upgrade';
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;

                proxy_pass http://localhost:3000;
        }

        location /myservice {
            rewrite ^/myservice/(.*)$ /$1 break;

            proxy_http_version 1.1;
            proxy_cache_bypass $http_upgrade;

            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;

            proxy_pass http://localhost:3001;
    }
}
