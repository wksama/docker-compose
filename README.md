<details>
<summary>目录结构</summary>
<pre><code>
.
├── config                                  #配置文件目录
│   ├── mysql                               #mysql配置文件
│   ├── nginx                               #nginx配置文件
│   ├── php56                               #php56配置文件
│   ├── php72                               #php72配置文件
│   ├── phpmyadmin                          #phpadmin配置文件
│   └── redis                               #redis配置文件
├── data                                    #数据存放目录
│   ├── mysql                               #mysql数据存放目录
│   └── redis                               #redis数据存放目录
├── docker-compose.yml.example              #docker-compose示例文件
├── dockerfiles                             #docker镜像构建目录
│   └── php                                 #php镜像构建目录
├── env.example                             #环境变量示例文件
├── log                                     #日志文件加
│   ├── nginx                               #nginx日志
│   └── php                                 #php日志
└── www                                     #代码存放目录
</code></pre>
</details>

### 使用

1. 安装docker
```
```

2. 克隆项目

```
$ git clone git@github.com:WencoChen/dnmp.git
```

3. 个性化配置

```
$ cd dnmp
$ cp docker-compose.yml.example docker-compose.yml
$ cp env.example .env
```

4. 运行

```
$ docker-compose up -d
```