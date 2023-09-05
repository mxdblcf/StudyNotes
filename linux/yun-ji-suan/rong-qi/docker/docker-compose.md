# docker-compose

## 快速使用yml来启动一个容器



### 使用docker-compose创建mariaDB

1.创建docker-compose.yml文件

<pre class="language-yaml"><code class="lang-yaml"><strong>version: '3'
</strong>services:
  mariadb:
    image: mariadb
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=your_root_password
      - MYSQL_DATABASE=your_database_name
      - MYSQL_USER=your_username
      - MYSQL_PASSWORD=your_password
    volumes:
      - ./data:/var/lib/mysql
    ports:
      - 3306:3306
</code></pre>

2.在该yml目录下输入命令拉取image

```bash
docker-compose up -d   #后台启动
```
