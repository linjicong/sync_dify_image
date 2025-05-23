# sync_dify_image

## 功能

- 从 Docker Hub 拉取镜像
- 将镜像推送到阿里云 ACR
- 支持通过 Docker Compose 文件自动解析和同步镜像

## 配置 GitHub Secrets

在 GitHub 仓库设置中，添加以下 secrets：

- `ACR_USERNAME`: 阿里云 ACR 用户名
- `ACR_PASSWORD`: 阿里云 ACR 密码
- `ACR_REGISTRY`: 阿里云 ACR 注册表地址（例如：`your-registry-id.cn-hangzhou.aliyuncs.com`）

## 工作流

GitHub Actions 工作流定义文件位于 `.github/workflows/sync-images.yml`。工作流的主要步骤如下：

1. **从 `dify` 仓库读取镜像**：工作流会检查 `langgenius/dify` 仓库中的代码，并读取 `docker/docker-compose.yaml` 文件中的镜像定义。
2. **解析 Docker Compose 文件**：使用 `yq` 工具从 `docker-compose.yaml` 文件中提取镜像名称。
3. **登录到阿里云 ACR**：使用配置的 GitHub Secrets 登录到阿里云 ACR。
4. **拉取、标记和推送镜像**：拉取 Docker Hub 上的镜像，标记并推送到阿里云 ACR。

## 使用

每当你将代码推送到 `main` 分支时，GitHub Actions 将自动执行上述工作流，确保镜像在 Docker Hub 和阿里云 ACR 之间保持同步。

| 源镜像                                          | 替换后镜像                                                     |
|-------------------------------------------------|----------------------------------------------------------------|
| langgenius/dify-api:1.3.1                     | registry.cn-hangzhou.aliyuncs.com/linjicong/dify-api:1.3.1     |
| langgenius/dify-web:1.3.1                     | registry.cn-hangzhou.aliyuncs.com/linjicong/dify-web:1.3.1    |
| postgres:15-alpine                              | registry.cn-hangzhou.aliyuncs.com/linjicong/postgres:15-alpine  |
| redis:6-alpine                                  | registry.cn-hangzhou.aliyuncs.com/linjicong/redis:6-alpine      |
| langgenius/dify-sandbox:0.2.10                   | registry.cn-hangzhou.aliyuncs.com/linjicong/dify-sandbox:0.2.10 |
| langgenius/dify-plugin-daemon:0.0.1-local        | registry.cn-hangzhou.aliyuncs.com/linjicong/dify-plugin-daemon:0.0.1-local |
| ubuntu/squid:latest                             | registry.cn-hangzhou.aliyuncs.com/linjicong/squid:latest |
| certbot/certbot                                 | registry.cn-hangzhou.aliyuncs.com/linjicong/certbot:latest |
| nginx:latest                                    | registry.cn-hangzhou.aliyuncs.com/linjicong/nginx:latest        |
| semitechnologies/weaviate:1.19.0                | registry.cn-hangzhou.aliyuncs.com/linjicong/weaviate:1.19.0 |
| langgenius/qdrant:v1.7.3                        | registry.cn-hangzhou.aliyuncs.com/linjicong/qdrant:v1.7.3      |
| pgvector/pgvector:pg16                          | registry.cn-hangzhou.aliyuncs.com/linjicong/pgvector:pg16 |
| tensorchord/pgvecto-rs:pg16-v0.3.0              | registry.cn-hangzhou.aliyuncs.com/linjicong/pgvecto-rs:pg16-v0.3.0 |
| ghcr.io/chroma-core/chroma:0.5.20                | registry.cn-hangzhou.aliyuncs.com/linjicong/chroma:0.5.20 |
| quay.io/oceanbase/oceanbase-ce:4.3.3.0-100000142024101215  |  registry.cn-hangzhou.aliyuncs.com/linjicong/oceanbase-ce:4.3.3.0-100000142024101215 |
| container-registry.oracle.com/database/free:latest | registry.cn-hangzhou.aliyuncs.com/linjicong/free:latest |
| quay.io/coreos/etcd:v3.5.5                      | registry.cn-hangzhou.aliyuncs.com/linjicong/etcd:v3.5.5 |
| minio/minio:RELEASE.2023-03-20T20-16-18Z        | registry.cn-hangzhou.aliyuncs.com/linjicong/minio:RELEASE.2023-03-20T20-16-18Z |
| milvusdb/milvus:v2.3.1                          | registry.cn-hangzhou.aliyuncs.com/linjicong/milvus:v2.3.1 |
| opensearchproject/opensearch:latest             | registry.cn-hangzhou.aliyuncs.com/linjicong/opensearch:latest |
| opensearchproject/opensearch-dashboards:latest  | registry.cn-hangzhou.aliyuncs.com/linjicong/opensearch-dashboards:latest |
| myscale/myscaledb:1.6.4                         | registry.cn-hangzhou.aliyuncs.com/linjicong/myscaledb:1.6.4 |
| docker.elastic.co/elasticsearch/elasticsearch:8.14.3 | registry.cn-hangzhou.aliyuncs.com/linjicong/elasticsearch:8.14.3 |
| docker.elastic.co/kibana/kibana:8.14.3          | registry.cn-hangzhou.aliyuncs.com/linjicong/kibana:8.14.3 |
| downloads.unstructured.io/unstructured-io/unstructured-api:latest | registry.cn-hangzhou.aliyuncs.com/linjicong/unstructured-api:latest |


