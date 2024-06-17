这是 Docker 的练习。

前后端两个容器并不直接访问各自提供的网络服务，_**前端的代码不是运行在前端的容器中，前端的代码，React APP 的代码实际上运行在浏览器上**_。前端的发起的所有的请求最终都会到 docker compose 的反向代理服务器。

> [!TIP]
> 什么是反向代理服务器?
> 
> 所有发送到反向代理服务器的请求，反向代理服务器决定这个请求发送给谁来处理。反向代理服务器运行在服务端，对客户端来说是透明的。

`docker-compose.dev.yml` 可以一键启动前后端的开发环境。但是还有一些不足之处：

- MongoDB 没有使用 Docker 容器，使用的是之前开发的时候用的在线的 MongoDB 服务 （后端的正常工作需要在 `.env` 中指定 `MONGODB_URL`）
- MongoDB URL 的设置没有通过 `docker-compose.dev.yml` 的环境变量(docker compose 也可以使用 .env 文件的)
- 没有支持 `docker compose up --build`，也就是说在 docker compose 之前我必须已经构建了需要的镜像

`docker-compose.yml` 可以一键启动 notes-app 的前端服务和后端服务（这个项目是前后端分离的），仍然有 `docker-compose.dev.yml` 的所有的不足点。

这个 todo-app 是根据课程内容和练习完成的是一个更完善的例子，但是其中的 `docker-compose.yml` 设置 `VITE_BACKEND_URL` 为 `/api` 而不指定域名和端口是比其中的 `docker-compose.dev.yml` 更好的做法，因为项目的前后端都是通过 Nginx 反向代理提供单一的访问入口。

https://github.com/wngtk/part12-containers-applications/tree/main/todo-app
