# Redpill_CustomBuild
[![](https://img.shields.io/github/issues-search?label=%E5%AE%9A%E5%88%B6%E6%AC%A1%E6%95%B0&query=repo%3Awjz304%2FRedpill_CustomBuild%20label%3Acustom)](https://github.com/wjz304/Redpill_CustomBuild/issues?q=label%3Acustom)
[![](https://img.shields.io/github/issues-search?label=%E6%AF%8F%E6%97%A5%E6%9E%84%E5%BB%BA&query=repo%3Awjz304%2FRedpill_CustomBuild%20label%3Aschedule)](https://github.com/wjz304/Redpill_CustomBuild/issues?q=label%3Aschedule)  

## 介绍  
[Redpill_CustomBuild](https://github.com/wjz304/Redpill_CustomBuild)  
一个自定义配置及驱动并通过 Github Action 编译 DSM redpill 引导的平台.  
本库并没有实际的技术创新, 仅做了一个参数适配, 使一些定制更简单, 并把过程搬到线上, 依赖微软强大的服务器使其快速得到想要的引导文件.  
高度依赖以下大佬的项目, 请给以下各位大佬点赞.
>源码仓库： [@RedPill-TTG](https://github.com/RedPill-TTG/redpill-load)  
>编译来源： [@pocopico](https://github.com/pocopico/redpill-load) [@jumkey](https://github.com/jumkey/redpill-load)  
>驱动来源： [@pocopico](https://github.com/pocopico/rp-ext)  

> 😎 为什么用 GitHub Action？  
> 托管于 GitHub 服务器, 只要 GitHub 不宕机, 它就不受影响(Private 项目每月有 2000 次的限制, Public 项目无限制).

## 链接
[【👉快速创建】](https://wjz304.github.io/Redpill_CustomBuild/Issues.html)  
[【👉快速创建】(dev)](https://wjz304.github.io/Redpill_CustomBuild/Issues.html?dev=1)  
`普通模式默认使用pocopico的驱动库, dev模式默认使用我fork的驱动库(如果报 Checksum 错, 请尝试使用(dev)模式), `  
`并发较多时, 有概率出现curl错误或者 未触发编译的情况, 过几分钟再试...`  
‼️‼️‼️  
`再次强调一下, 本项目全部代码和过程为公开状态, SN & MAC 自定义有泄露的风险, 如涉及个人财产尽量不要填写, 或者fork到自己名下操作.`

## 使用  
在本项目 Issues 中创建问题(符合下述规范), 按需填写即可发起定制构建[【👉图文说明】](https://github.com/wjz304/Redpill_CustomBuild/blob/main/guide/Issues.md) [【👉注意事项】](https://github.com/wjz304/Redpill_CustomBuild/blob/main/tips.md).  

### Issue title:
标题请以 custom 开头(不区分大小写), 且不要包含'(单引号),"(双引号) 等转义字符.
### Issue body:
内容 以json格式编写(切记符号为英文符号, [【👉JSON检测】](https://json-online.com/check/))

参数      | 必选  |     默认值     | 说明  
----------|------|----------------|---------
platform  | √    |"DS3622xs+"     | 选择你需要编译的型号. "DS918+", "DS920+", "DS1621+", "DS3615xs", "DS3617xs", "DS3622xs+", "DVA1622", "DVA3221"  
version   | √    |"7.0.1-42218"   | 选择你需要编译的版本. "7.1.1-42962", "7.1.0-42661", "7.0.1-42218", "6.2.4-25556"  
config    | ×    |-               | 更新 user_config.json 参数 [①]  参考[#931](https://github.com/wjz304/Redpill_CustomBuild/issues/931)
map       | ×    |-               | 控制器盘数(SataPortMap)和盘序(DiskIdxMap)两个字段, 并以","间隔. eg: "1,00"  
dtb       | ×    |-               | dtb文件下载URL(support ext: .dts,.dtb,.tar.gz,.zip) [#47](https://github.com/wjz304/Redpill_CustomBuild/issues/47)
sn        | ×    |-               | 序列号. 默认根据型号随机生成. eg: "1980PDN002189" 
mac       | ×    |-               | MAC地址. 多个请以 "," 间隔. 默认根据型号随机生成. eg: "001132888A95, 001132888A96"  
usb       | ×    |"0x0001, 0x46f4"| 设备识别码（pid）和供应商ID（vid）[格式: pid, vid]. 默认无.  eg: "0xa4a5, 0x0525"  
ext       | ×    |-               | 多个请以 "," 间隔. 支持名字（pocopico库）或者链接，名字参考[rp-ext](./exts.json). eg: "r8125, tg3", 链接参考[#753](https://github.com/wjz304/Redpill_CustomBuild/issues/753)  
exp       | ×    |"pocopico"      | 编译依赖的基础库. "pocopico", "jumkey" (大佬的抉择，7.1 优先选 pocopico, 7.0-jun 优先选 jumkey)
jun       | ×    |"0"             | 仅7.0.1-42218 版本可以选择jun模式，jun模式 支持 7.0.1~7.1.1 的 DSM。
\-        | ×    |-               | 高级自定义 [②]  

```
  *①: 格式 json, key会更新到默认的user_config.json中, 因此请谨慎编写.
    - 比如 想修改 maxlanport, 需要填写完整的 synoinfo 属性, 当仅填写 {"synoinfo": {"maxlanport": "8"}} 时, 将更新 synoinfo 为只有 maxlanport, 原有 internalportcfg 将会丢失.
  *②: body 中可直接插入shell脚本："由于权限太高, 防止有些人执行非法操作, 仅仓库作者可操作, 请联系该仓库管理员或者fork到自己名下操作."   
    - 在 body 中 以 ```xxx``` 包裹自定义的 shell 命令, 将在 build 前运行. 参考[#3](https://github.com/wjz304/Redpill_CustomBuild/issues/3) 
```

## 说明
0. __感谢 [hoping](https://github.com/htmambo) 大佬制作的 WEB 界面.__  
1. 构建成功 Issues 会自动 closed.  
2. 构建失败 后请调整参数重新创建Issues发起重新构建, 或者修改body后 Close Issue + Reopen 重新触发.（触发编译：open, reopen）. 
3. 再次构建, 直接 reopen 会再次触发构建. 
4. 每日构建, 打上'schedule' [【👉标签说明】](https://github.com/wjz304/Redpill_CustomBuild/blob/main/guide/Issues.md#issues-%E6%AF%8F%E6%97%A5%E5%BE%AA%E7%8E%AF%E6%9E%84%E5%BB%BA%E6%95%99%E7%A8%8B)标签 将会每日构建(通过Reopen的方式, 因此如果构建失败Issues没有Closed 将终止).  
5. 驱动的选择请参考[【👉驱动列表】](https://xpenology.com/forum/topic/4980-gt-hardware-supported-list-for-dsm-52-lt/).     
6. 根据github官方说明所有的编译结果保留90天，周知.
7. 如果没有魔法, 附件下载不下来, 请在 Issue 中回复 'transfer' 使用快传, 或者参考 https://github.com/wjz304/hosts 设置 hosts.
8. [【👉问题反馈】](https://github.com/wjz304/Redpill_CustomBuild/issues/807)  交流群 QQ群: [21609194](https://qm.qq.com/cgi-bin/qm/qr?k=8AU8VJ82OR2HB_77g3vsjGKA-rm-p67B&jump_from=webapi)  TG: [https://t.me/Redpill_CustomBuild](https://t.me/Redpill_CustomBuild)  
 `(PS: 在Issues上评论我可能看不到, 邮件太多了, 如长时间未回复请私信.)`  
9. fork 本项目 Issues 和 Action 使用没有问题的.  
  但是快速创建的WEB页面由于 涉及 guthub 的 pages, 且含有CDN加速, 存在一些硬编码, 如要使用, 需要开通pages后修改指向方可使用.  


## 举例
* 普通参数示例:
  - {"platform":"DS3622xs+", "version":"7.0.1-42218", "ext":"r8125, tg3"}  
  - {"platform":"DS3622xs+", "version":"7.0.1-42218", "exp": "jumkey", "jun":"1", "ext":"r8125, tg3"} 
  - {"platform":"DS3622xs+", "version":"7.0.1-42218", "map":"1,00", "usb":"0xa4a5, 0x0525"}  
  - {"platform":"DS3622xs+", "version":"7.1.0-42661", "sn":"1980PDN002189", "mac":"001132888A95","ext":"r8125"}   
  - {  
      "platform":"DS3622xs+",  
      "version":"7.0.1-42218",  
      "jun":"1",  
      "exp": "jumkey",  
      "mac":"001132888A95, 001132888A96, 001132888A97",  
      "ext":"r8125, r8168, e1000e, igb, vmxnet3, ixgbe"  
    }  
* dtb参数示例:
  - {"platform":"DS920+",  
      "version":"7.0.1-42218",  
      "dtb": "https://github.com/wjz304/Redpill_CustomBuildfiles/9235785/ds920p.zip",  
      "ext":"r8125"
    }  
* ext参数链接示例:
  - {  
      "platform":"DS3622xs+",  
      "version":"7.1.1-42962",  
      "ext":"r8125, e1000, e1000e, vmxnet3, https://raw.githubusercontent.com/wjz304/rp-ext/main/rtl8150/rpext-index.json"  
    }
* config参数示例:
  - {  
      "platform":"DS3622xs+",  
      "version":"7.0.1-42218",  
      "config":{"synoinfo": {"maxlanport": "4","esataportcfg": "0xfffc","internalportcfg": "0x3","maxdisks": "16"}},  
      "ext":"r8125, e1000, e1000e, vmxnet3"  
    }  
* 高级自定义示例:
  - {"platform":"DS3622xs+", "version":"7.0.1-42218", "jun":"1", "ext":"r8125,e1000e,vmxnet3"}  
    \`\`\`  
    echo "${platform}"  
    \`\`\`  
    
</br>
<details><summary>🍻打赏一下</summary>  
<div><img src="https://raw.githubusercontent.com/wjz304/wjz304/master/my/20220908134226.jpg" width="500"></div>  
</details>  
</br>

## 鸣谢
https://github.com/RedPill-TTG/redpill-load  
https://github.com/jumkey/redpill-load  
https://github.com/pocopico/redpill-load  
https://github.com/Online24Hours/Redpill_Build  
