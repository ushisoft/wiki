# 常用镜像

#### Nginx

##### Javadoc

```bash
docker run --name javadoc-nginx -p 88:80 -v /tmp/javadoc:/usr/share/nginx/html:ro -d nginx
```

