## 项目组成

本项目是一个全栈的待办事项应用，包括：

- `client` 是 React + Redux 编写的前端页面
- `server` 是 Express 实现的 API 服务器

数据库则是使用 MongoDB。

## 运行项目

请先安装 [Docker](https://www.docker.com/)，然后运行以下命令：

```bash
# 创建网络，便于容器互联
docker network create dream-net

# 启动 MongoDB 容器（dream-db）
docker run --name dream-db --network dream-net -d mongo

# 构建 Express API 服务器
docker build -t dream-server server/

# 启动 Express API 容器（dream-api）
docker run -p 4000:4000 --name dream-api --network dream-net -d dream-server

# 构建提供 React 前端页面的 Nginx 服务器
docker build -t dream-client client/

# 启动 Nginx 服务器容器（client）
docker run -p 8080:80 --name client -d dream-client
```

然后访问 `localhost:8080`，就可以进入应用。

