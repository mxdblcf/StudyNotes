# CDN

CDN的基本原理

就近访问资源，分布式多节点分摊源站压力

<figure><img src="../../.gitbook/assets/CDN架构.svg" alt="" width="563"><figcaption><p>CDN arch</p></figcaption></figure>

## 302调度&#x20;

基于内容和精准ip实现的调度，分配最优ip给client （会使url地址发生变化）

## CDN排障

#### 1.curl测试节点异常（例如:https://xxx.com/xx.jpg访问出问题）

从边缘节点，中间源，源站一层一层查，获得其节点IP,然后代理访问

https的话： curl https://xxx.com/xx.jpg --resolve xxx.com:443:\<ip地址>

http的话： curl http://xxx.com/xx.jpg -x \<IP地址>:80

curl -I 可以看到是否cache hit,这个也很关键，没有cache的话可能是回源有问题，检查回源host配置

&#x20;





## 企业使用CDN的成本优化

* 内网请求避免走CDN
* 客户端强制缓存
* 使用gzip br压缩 智能压缩
* 开启http2 quic
* 图片格式转WEBP
