# DeployMiddleware

本项目使用 docker-compose 配置开发环境，集成了常用的基础服务。目前包含：

- PostgreSQL: 关系型数据库
- Redis: 内存数据库/缓存
- MinIO: 对象存储服务

后续可以根据需求轻松扩展更多服务。

## 项目结构

```
├── docker-compose.yml          # Docker 编排配置文件
├── README.md                   # 项目说明文档
├── postgres/                   # PostgreSQL 相关文件
│   ├── data/                   # 数据文件
│   ├── conf/                   # 配置文件
│   └── init-scripts/           # 初始化脚本
├── redis/                      # Redis 相关文件
│   ├── data/                   # 数据文件
│   └── conf/                   # 配置文件
└── minio/                      # MinIO 相关文件
└── data/                   # 数据文件
```

## 操作指南


- 启动服务：

```bash
docker-compose up -d
```

- 停止服务：

```bash
docker-compose down
```

- 重启服务：

```bash
docker-compose restart
```

- 查看服务状态：

```bash
docker-compose ps
```

- 查看服务日志：

```bash
docker-compose logs -f [service_name]
```

### 更新服务

1. 修改 docker-compose.yml 中的镜像版本
2. 执行更新命令：

```bash
docker-compose pull   # 拉取新镜像
docker-compose up -d  # 重新创建容器
```

### 数据备份

- PostgreSQL 备份：

```bash
docker-compose exec postgres pg_dump -U myuser mydatabase > backup.sql
```

- Redis 备份：
  Redis 已配置 AOF 和 RDB 持久化，数据存储在 redis/data 目录
- MinIO 备份：
  数据存储在 minio/data 目录，可直接备份该目录
