## 应用程序区分：  
    有状态：一个应用程序处理请求时，与曾经处理的请求有关联关系  
    无状态：一个应用程序处理请求时，与曾经处理的请求无关联关系，每个请求都是独立的  

## 运维三大核心任务：发布、变更、故障处理   
    人肉运维：重复、易出错   
    脚本化运维：重复造轮子   
    专业运维系统：  
    云计算系统：  
        openstack（kvm，xen等主机级虚拟化）  
        容器编排系统  
            docker-compose，docker-swam（cluster），docker-machine  
            mesos（DC/OS），marathon  
            kubernetes，Google（Borg），golang语言研发  
        滚动更新、变更（HPA）、故障处理  
    
## 容器编排  
    Docker通过“镜像”机制极富创造性地解决了应用程序的根本性难题，它推动了容器技术的快速普及生产落地；
    容器本身仅提供了托管运行应用的底层逻辑，而容器编排（Orchestration）才是真正产生价值的位置所在；
    
    1.管理容器的运行生命周期
    2.提供、部署容器运行起来
    3.管理容器的冗余和可用性
    4.通过向上、或分散到多个主机上完成扩展
    5.如果主机宕机，则把对应容器迁移到存活的主机上
    6.整个集群中有限的计算资源在多个容器之间完成合理分配
    7.所有容器仅需要把代理服务器暴露出去
    8.负载均衡、服务注册、服务发现，容器是动态的
    9.监控容器及各宿主机的监控状态
    10.配置应用程序并确保容器之间的关联关系得到呈现

    Service Discovery
    Load Balancing
    Secrets/configuration/storage management
    Health checks
    Auto-[scaling/restart/healing] of containers and nodes
    Zero-downtime deploys

    实现：
        自动装箱，自我修复，水平扩展，服务发现和负载均衡，自动发布和回滚
        密钥管理和配置管理，存储编排

## k8s发行版  
    RedHat：OpenShift
    Rancher：

## k8s集群节点
    master：主节点（一般3个）
        api server：负责接收创建容器请求，restful 风格
        scheduler：集群资源掌控，资源调度
        controller-manager：控制器管理器，确保容器处于健康状态
    node：工作节点（众多工作节点组成一个集群）
        kubelet:接受任务，启动，管理容器等
        容器引擎：docker

    pod：k8s调度的单元，容器的外壳、pod给容器做了一个封装。同一组容器在一个pod内共享同一个网络名称空间，mat、uts、ipc。user、mnt、pid互相隔离。共享存储卷。   
    为了便于管理，还需要给pod打上标签，方便基于标签识别、管理pod    
        label--> 标签选择器   
