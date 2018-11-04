ansible是DevOps项目基础支撑工具之一，是第一款实现读/写跨平台的"Infrastructure as code"工具，从系统管理者到开发者，都可以用Ansible自动部署并维护整个应用的生命周期，实现持续交付。

可支持云环境应用部署。


优点：
ansible的编排引擎可以出色地完成配置管理、流程控制、资源部署等多方面工作。与其他IT自动化产品相比较
1. 无需安装客户端软件，管理简便，功能强大的基础架构配置、维护工具。
2. 基于描述基础架构的语言无论对机器还是人都是友好的。
3. 简单易用的IT自动化系统。

## inventory文件
是一个INI的静态文件
```
[docker]
172.17.42.10[1:3]
```

```shell
ansible docker -m ping -o
```

动态inventory：支持主机列表和变量信息从外部拉取，然后用Ansible进行管理。
操作：把ansible.cfg文件中的inventory的定义值改成可执行脚本即可。

## Ad-Hoc命令
-B SECONDS
-m MODULE_NAME
-P POLL_INTERVAL
-a MODULE_ARGS
-f FORKS
-o 压缩输出

## Ansible playbook
是ansible进行配置管理的组件。

## Ansible facts信息
facts组件是ansible用于被管机器设备信息的一个功能。可以使用filter来查看指定的信息。
放在一个json格式的数据结构中

把facts信息作为playbook变量信息进行引用
用facter来扩展facts信息
```
ansible IP_ADDRESS -m setup
```
## Ansible role
role只是对日常使用的playbook的目录结构进行一些规范
site.yaml 是role引用的入口文件
handlers目录 存放一些task的handler
files目录 存放静态文件
tasks目录 存放playbook中的task
templates目录 存放jinja2模板文件
vars目录 存放变量文件
