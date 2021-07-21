# prometheus-thanos

## 版本
* prometheus:v2.15.2
* thanos-0.17.2
* consul v1.9.4
* consul-template v0.25.2

## 架构选型参考
如果你的 Query 跟 Sidecar 离的比较远，比如 Sidecar 分布在多个数据中心，Query 向所有 Sidecar 查数据，速度会很慢，这种情况可以考虑用 Receiver，将数据集中吐到 Receiver，然后 Receiver 与 Query 部署在一起，Query 直接向 Receiver 查最新数据，提升查询性能。
如果你的使用场景只允许 Prometheus 将数据 push 到远程，可以考虑使用 Receiver。比如 IoT 设备没有持久化存储，只能将数据 push 到远程。

## sidecar
* prometheus、thanos-sidecar 部署到一起
* thanos-query独立部署

## receiver
* 因为使用了 Receiver 来统一接收 Prometheus 的数据，所以 Prometheus 也不需要 Sidecar 了，但需要给 Prometheus 配置文件里加下 remote_write，让 Prometheus 将数据 push 给 Receiver:

## 存储
* objectstorage.service为本地存储，测试使用
* s3.yaml为远端存储，生产环境科研
