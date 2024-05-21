# eclipse-mosquitto:2.0.18

## 镜像中创建了三个目录，用于配置、持久存储和日志

```sh
# 启动一个最基本的容器, 目的是拷贝出来默认的配置文件
docker run -d --name eclipse-mosquitto_temp eclipse-mosquitto:2.0.18
docker cp eclipse-mosquitto_temp:/mosquitto/config/mosquitto.conf /"$PWD"/eclipse-mosquitto/config
docker stop eclipse-mosquitto_temp && docker rm eclipse-mosquitto_temp

# 启动容器
docker run -d -p 1883:1883 \
  -v /"$PWD"/eclipse-mosquitto/config:/mosquitto/config \
  -v /"$PWD"/eclipse-mosquitto/data:/mosquitto/data \
  -v /"$PWD"/eclipse-mosquitto/log:/mosquitto/log \
  --name eclipse-mosquitto_2.0.18 \
  eclipse-mosquitto:2.0.18

# 进入容器
docker exec -it eclipse-mosquitto_2.0.18 /bin/sh
```