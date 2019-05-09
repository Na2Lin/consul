## consul集群搭建
### 安装consul
* [下载地址](https://www.consul.io/downloads.html)(作为初学者尽量不要下载最新版本),根据自身系统选择下载.zip文件.
* 解压下载的.zip文件,并配置环境变量.
### 启动server节点
```
consul agent -server -bootstrap-expect 2 -data-dir /tmp/consul/data -bind=192.168.1.10 -node=s1 [-retry-join xxx.xxx.xx.xx] -client 0.0.0.0
```
- -server: server节点标识,没有该参数表示为client节点
- -bootstrap-expect: 集群期望的节点数,大于1时会等待其他节点加入后正式启动集群
- -data-dir: 数据文件路径
- -bind: 其他所有节点可访问的本机ip
- -node: 节点名称
- -client: 可访问地址,配置0.0.0.0表示可任意访问.
- 其他server节点启动后,新开终端执行:
```consul join 192.168.1.10(第一个启动的server节点bind的ip)```,也可以在启动时添加-retry-join 参数,值为join节点bind的ip
### 启动client节点
```
consul agent -data-dir /tmp/consul/data -bind=192.168.1.12 -node=c1 -retry-join 192.168.1.10 -client 0.0.0.0 
```
### 查看集群节点:
```
consul members
```
   
    
