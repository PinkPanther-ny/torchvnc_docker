Run script to create docker with specific port, connect via vnc software.  
  
```
git clone https://github.com/PinkPanther-ny/torchvnc_docker  
cd torchvnc_docker && ./create_test_vnc_docker.sh  
```
  
运行后自动将```torchvnc_docker```此目录在container中链接到```/datav```  
另外，主机的根目录```/```链接到container中的```/host_root_dir```
以便于浏览数据及其他操作，需谨慎。  
  
远程桌面直接用vnc软件连接 {主机ip}：{端口前缀}+90  
  
====================================================================  
  
登陆后如果想从ssh连接，需通过```passwd```设置用户ssh密码（非vnc密码）  
另外需修改```/etc/ssh/sshd_config```中的配置  
```PermitRootLogin yes  ```  
然后运行```/etc/init.d/ssh restart```即可  
  
首次进入container建议运行```conda init```  
conda环境中自带python3.9，pytorch1.11+cu113，以及opencv  
  
====================================================================  
  
docker_images目录下的两个Dockerfile则是如何构建此镜像的源码，可以用来学习dockerfile的基本操作  
  
====================================================================  
  
另附上container中ngrok内网穿透的配置，vpn文件夹映射到```/datav/vpn```文件夹中  
建议在```tmux```或```screen```中运行
```
cd /datav/vpn && ./run_vpn.sh
```
运行后可内网外远程访问vnc，ssh，以及http服务等
 
```
# Note that remote port if not specified, it will be assigned automatically

server_addr: "zifuture.com:988"  
tunnels:  
  vnc:  
    proto:  
      tcp: 5900  
    remote_port: {自定义vnc连接zifuture的端口号}  
  ssh:  
    proto:  
      tcp: 22  
    remote_port: {自定义ssh连接zifuture的端口号}  
  
  tensorboard_or_jupyterhub:  
    proto:  
      http: 6006  
    remote_port: {自定义ssh连接jupyterhub或者其他网络服务的端口}  
```
  
--Alvin  
  
