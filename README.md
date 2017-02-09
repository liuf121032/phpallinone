# 舟哥全功能PHP栈 nICKZHUO_PHP_FULL_STACK_ALL_IN_ONE
## 说明
基于Docker的PHP7.1容器，专为Symfony设计。

## 配置
* Nginx: 1.11.9
* PHP: 7.1.1
* Redis客户端: 3.0.0
* Composer: 最新版
* Swoole: 2.0.5


## 详细说明
* 专门为了跑symfony做的容器，一个nginx，一个php7fpm，以及PHP的周边扩展。为了更好的兼容（docker中volume顺序会导致chown权限丢失等问题），去掉了volume的挂载，作为base镜像，建议在子镜像中开启挂载或者手工命令行挂载，避免问题。
* 请将自己的symfony项目放到/data/www目录，配合启动命令启动。
* 包含了持续集成能力（daocloud)

## 目录结构说明
* code - 存放了一个phpinfo的查看演示文件，启动之后80端口显示。
* Dockerfile - 构建镜像文件，所有的部署命令
* scripts - 存放镜像构建用的命令以及entrypoint.sh和初始化CMD脚本（生产和测试）
* conf - 存放默认配置，包含nginx和supervisord。
* env - 存放一些用户讯息例如vim配置等，方便调试，生产环境不会用到。

## 使用说明
* 可以fork或者基于该镜像制作子镜像。
* 参考快速使用说明，直接使用本镜像。

## 快速使用说明
* 可以使用 docker build 命令来构建属于自己的本地镜像，但是原则上不推荐，考虑到速度以及docker版本差异等。
* 推荐使用在公开仓库发布的最新镜像，如下操作步骤。
1. 启动 docker run -p 80:80 -v {项目在本地路径}:/data/www/ --name=myphp daocloud.io/artsky/phpallinone:latest 
2. docker exec -it myphp bash 进入容器内
3. 修改项目相应的配置文件
4. 容器内修改权限 chown -R www:www /data/www
5. 来到容器内/data/www目录下运行 composer install 更新依赖关系
6. 打开本地80口访问