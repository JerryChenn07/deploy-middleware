# DeployMiddleware

本项目使用 docker-compose 配置开发环境，集成了常用的基础服务。目前包含：

- PostgreSQL: 关系型数据库
- MySQL: 关系型数据库
- Redis: 内存数据库/缓存
- MinIO: 对象存储服务

后续可以根据需求轻松扩展更多服务。

## 项目结构

```
├── postgres.yml                # PostgreSQL 服务配置文件
├── mysql.yml                   # MySQL 服务配置文件
├── redis.yml                   # Redis 服务配置文件
├── minio.yml                   # MinIO 服务配置文件
├── README.md                   # 项目说明文档
├── postgres/                   # PostgreSQL 相关文件
│   ├── data/                   # 数据文件
│   ├── conf/                   # 配置文件
│   └── init-scripts/           # 初始化脚本
├── mysql/                      # MySQL 相关文件
│   ├── data/                   # 数据文件
│   └── conf/                   # 配置文件
├── redis/                      # Redis 相关文件
│   ├── data/                   # 数据文件
│   └── conf/                   # 配置文件
└── minio/                      # MinIO 相关文件
    └── data/                   # 数据文件
```

## 操作指南

每个服务都有独立的配置文件（postgres.yml、mysql.yml、redis.yml、minio.yml），您可以根据需要选择启动单个或多个服务。

- 启动单个服务：

```bash
docker-compose -f <服务配置文件> up -d

# 示例：启动 PostgreSQL
docker-compose -f postgres.yml up -d

# 示例：启动 MySQL
docker-compose -f mysql.yml up -d

# 示例：启动 Redis
docker-compose -f redis.yml up -d

# 示例：启动 MinIO
docker-compose -f minio.yml up -d
```

- 启动多个服务：

```bash
docker-compose -f <服务1配置文件> -f <服务2配置文件> up -d

# 示例：同时启动 PostgreSQL 和 Redis
docker-compose -f postgres.yml -f redis.yml up -d
```

- 停止服务：

```bash
docker-compose -f <服务配置文件> down

# 示例：停止 PostgreSQL
docker-compose -f postgres.yml down
```

- 重启服务：

```bash
docker-compose -f <服务配置文件> restart
```

- 查看服务状态：

```bash
docker-compose -f <服务配置文件> ps
```

- 查看服务日志：

```bash
docker-compose -f <服务配置文件> logs -f [service_name]
```

### 更新服务

1. 修改对应服务的配置文件中的镜像版本
2. 执行更新命令：

```bash
docker-compose -f <服务配置文件> pull   # 拉取新镜像
docker-compose -f <服务配置文件> up -d  # 重新创建容器
```

### 数据备份

- PostgreSQL 备份：

```bash
docker-compose exec postgres pg_dump -U myuser mydatabase > backup.sql
```

- MySQL 备份：

```bash
docker-compose exec mysql mysqldump -u root -p mydatabase > backup.sql
```

- Redis 备份：
  Redis 已配置 AOF 和 RDB 持久化，数据存储在 redis/data 目录

- MinIO 备份：
  数据存储在 minio/data 目录，可直接备份该目录
