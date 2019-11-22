# HPA（horizontal pod autoscalar）

## 中间层 service
在提供服务的POD 以及 客户端之间增加一个固定的层

*  对客户端提供稳定的服务的入口
*  service讲服务代理到后端的pod之上  根据pod的label识别（标签选择器）
*  service其本质就是一组规则  1.12以后  相当于IPVS规则 IPVS负载均衡 https://www.cnblogs.com/hongdada/p/9758939.html
*  IP 和 service名称通过K8s的DNS进行解析

# AddOns： 附件
例如 DNS 动态更改（自身也是一个pod） 

 

# NMT 

<center>  <!--开始居中对齐-->

![GitHub set up](./01-&#32;NMT.png "NMT")

</center> <!--结束居中对齐-->

pod 创建通过对应的控制器（例如  ngnix控制器）
service  手动改创建 （k8s内部pod访问  k8s外部访问）

# k8s 的通信方式
* 同一个POd内的通信 lo（提供一个回环接口）
* 各Pod之间通信：  overlay Network 叠加网络
* pod 和 service之间的通信   pod网络和service网络  不在同一网络  iptabels  每个pod有一个组件 kube-proxy

# DNS server
共享存储 K8s 的etcd（键值存储） 一个端口用内部通信（点对点证书）  一个端口对外提供通信（与API server通信） 


# CNI container network interface(容器网络接口)
K8s 的网络解决方案  作为附件使用（AddOns）
* flannel: 网络配置
* calico： 网络配置  网络策略 
* canel： 利用fannel提供网络配置 利用calico提供网络策略
* ....

两种方式  可以作为附件运行 可以作为Node的守护进程运行
![net](./01&#32;k8s-net.png)


# K8s 空间
作为管理边界 
例如 开发空间  测试空间 通过网络策略实现空间直接是否可以通信

