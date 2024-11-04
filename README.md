### 自用面板

- 安装docker
```
curl -fsSL https://get.docker.com | sh
```

- 部署面板
```
docker run -d \
    --name app \
    -p 5000:5000 \
    -e ANSIBLE_HOST_KEY_CHECKING=False \
    -e ADMIN_USERNAME=admin123 \
    -e ADMIN_PASSWORD=admin123 \
    -v ./db:/app/db \
    ghcr.io/admin8800/ansible
```
