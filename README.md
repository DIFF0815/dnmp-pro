# 环境说明
环境原始来自[dnmp](https://github.com/yeszao/dnmp) ,稍做修改


## debug调试
* 推荐使用 Yasd 进行 Swoole 调试，类似 Xdebug，完美支持协程，支持断点调试、单步追踪、watch 变量；
* php.ini 配置添加下面内容
  ```shell
    zend_extension=yasd.so
    ;使用远程调试远程调试
    yasd.debug_mode=remote
    ;本地开发地址 IDE所在的ip地址，如果是虚拟机，请填写虚拟机和宿主机通信的那个网卡的ip地址
    yasd.remote_host=host.docker.internal
    ;本地开发监听端口
    yasd.remote_port=9901
    ; 这样的话,相当于默认开启了php -e选项, 调试完记得注释掉
    yasd.open_extended_info=1
  ```
* docker-composer.yml文件修改如下
  ```shell
    #php74下面添加
    environment:
      XDEBUG_CONFIG: "idekey=PHPSTORM"
      PHP_IDE_CONFIG: "serverName=phpIde"
  ```
* .env文件里面添加yasd扩展
* 重新build镜像和重启容器
* nginx配置添加特殊处理如下,重启配置
  ```shell
  # 域名加上host.docker.internal
  server_name hyperf-log-local.rotom-x.com host.docker.internal;
  ```
* 配置phpstrom [参考1](https://github.com/swoole/yasd/issues/136) [yasd](https://github.com/swoole/yasd)
* 