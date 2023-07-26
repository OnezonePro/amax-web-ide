
## 一、开发环境准备

1、安装浏览器插件gitpod [GitpodInstall.md](./GitpodInstall.md)

2、打开ide github项目，点击Gitpod，创建自己的工作空间 [https://github.com/armoniax/amax-web-ide](https://github.com/armoniax/amax-web-ide)

![image](https://github.com/OnezonePro/amax-web-ide/assets/80018598/a52f0d14-d32b-4994-b5fa-cbcb9fb3a1c9)

创建后

![image](https://github.com/OnezonePro/amax-web-ide/assets/80018598/aea02a22-c165-4a5d-9412-0169f1d7a7ef)


（在工作空间中，已经安装好了相关的环境，启动了本地节点）

3、完成合约开发和编译后，部署合约、调用合约：

```
amcli set code talk talk.wasm
amcli set abi talk talk.abi
amcli push action talk post '[1000, 0, bob, "This is a new post"]' -p bob
```
具体参照 [test-talk.sh](./test-talk.sh)

4、amcli [操作文档节点命令操作文档](https://armonia.gitbook.io/amax-dao-dev/v/chinese-1/fundamentals/amax-zhi-neng-he-yue-kai-fa/jie-dian-rpc-jie-kou-cao-zuo-ming-ling-da-quan)

## 二、ARC20合约开发示例

1、在contract目录下，已存在代码文件 arc.token.hpp、arc.token.cpp

2、编译合约

```
amax-cpp contract/arc.token.cpp
```

3、部署合约

```
amcli create account amax arc.token AM6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV

amcli set code arc.token arc.token.wasm
amcli set abi arc.token arc.token.abi
```

4、测试验证合约功能

```
amcli push action arc.token create '[ "amax", "1000000000.00000000 AMAX"]' -p arc.token@active
amcli push action arc.token issue '[ "amax", "1000000000.00000000 AMAX", "amax issue"]' -p amax@active
amcli push action arc.token transfer '["amax","myusermyuser","100.00000000 AMAX",""]' -p amax@active
amcli get table arc.token myusermyuser accounts
```

## 三、部署到测试链、主链

1、导入所需账号私钥

> amcli wallet import --private-key $private_key

2、部署测试链，只需指定测试链节点url

```
amcli -u http://test-chain.ambt.art set code arctoken1111 arc.token.wasm
amcli -u http://test-chain.ambt.art set abi arctoken1111 arc.token.abi 
```

3、部署到主网，改成 
> amcli -u http://expnode.amaxscan.io 

即可
