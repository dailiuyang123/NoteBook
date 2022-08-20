### docer 内启动 redis 服务指令：
  ``` docker run -d --name redis -p 6379:6379 redis:latest redis-server --appendonly yes --requirepass "你的密码" ```
  # 参数说明
  docker run -d ：后台运行

  --name redis：服务名

  -p 6379:6379    ： 将容器6379端口映射到主机6379端口  <a href="">注意：绑定后，将docker服务映射到本地计算器对应端口上，IP是本地计算机的ip</a>

  redis-server --appendonly yes：在容器执行redis-server启动命令，并打开redis持久化配置

  --requirepass "你的密码" ：设置密码
