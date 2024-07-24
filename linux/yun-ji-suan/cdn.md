# CDN

## CDN的基本原理

就近访问静态资源，分布式多节点分摊源站的压力

<figure><img src="../../.gitbook/assets/CDN架构.svg" alt="" width="563"><figcaption></figcaption></figure>

## CDN302调度

* 概念：基于内容和精准ip实现的调度，分配最优ip给client （会使url地址发生变化）
* 与dns调度区别:用户访问url第一次返回的不是资源ip，而是调度机ip，然后再向调度机ip request ，CDN厂商根据用户ip返回最优调度ip给用户来访问
* 适用：大流量分发，比如热点新闻要上线，使用302调度分摊服务器压力
* 注：暂没有实际接触，后续更新例子，有接触过的伙伴也可以提issue来丰富笔记

## CDN排障

#### 1.curl测试节点异常（例如:https://xxx.com/xx.jpg访问出问题）

从边缘节点，中间源，源站一层一层查，获得其节点IP,然后代理访问

https的话： curl https://xxx.com/xx.jpg --resolve xxx.com:443:\<ip地址>

http的话： curl http://xxx.com/xx.jpg -x \<IP地址>:80

curl -I 可以看到是否cache hit,这个也很关键，没有cache的话可能是回源有问题，检查回源host配置


## 企业使用CDN的成本优化

* 内网请求避免走CDN
* 客户端强制缓存
* 使用gzip br压缩 智能压缩
* 开启http2 quic
* 图片格式转WEBP
