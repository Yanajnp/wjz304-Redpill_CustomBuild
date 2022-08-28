# Redpill_CustomBuild

## 介绍  
[Redpill_CustomBuild](https://github.com/wjz304/Redpill_CustomBuild)

[![](https://img.shields.io/github/issues-search?label=%E5%AE%9A%E5%88%B6%E6%AC%A1%E6%95%B0&query=repo%3Awjz304%2FRedpill_CustomBuild%20label%3Acustom)](https://github.com/wjz304/Redpill_CustomBuild/issues?q=label%3Acustom)
[![](https://img.shields.io/github/issues-search?label=%E6%AF%8F%E6%97%A5%E6%9E%84%E5%BB%BA&query=repo%3Awjz304%2FRedpill_CustomBuild%20label%3Aschedule)](https://github.com/wjz304/Redpill_CustomBuild/issues?q=label%3Aschedule)

## 说明  
方式一：  
在本项目 Issues 中创建问题，按需填写即可发起定制构建。  
【👉[快速创建](https://wjz304.github.io/Redpill_CustomBuild/Issues.html)】 【👉[图文说明](https://github.com/wjz304/Redpill_CustomBuild/blob/main/guide/Issues.md)】 【👉[参考示例issue#1](https://github.com/wjz304/Redpill_CustomBuild/issues/1)】  【👉[驱动支持表](https://xpenology.com/forum/topic/4980-gt-hardware-supported-list-for-dsm-52-lt/)】  【👉[json错误检测](https://json-online.com/check/)】  

__感谢 [hoping](https://github.com/htmambo) 大佬制作的 UI界面__  

1. 构建成功 Issues 会自动 closed。  
2. 构建失败 后请调整参数重新创建Issues发起重新构建, 或者修改body后 Close Issue + Reopen 重新触发。（触发编译：open, reopen）。  
3. ext 存在兼容性问题, 添加时请与型号和版本对应, 并酌情添加 (不恰当的例子：r8125 不支持 DS920+ 的 7.0.1-42218 版本, 添加会编译失败)  
4. 再次构建，直接 reopen 会再次触发构建。
5. 打上 ['schedule'](https://github.com/wjz304/Redpill_CustomBuild/blob/main/guide/Issues.md#issues-%E6%AF%8F%E6%97%A5%E5%BE%AA%E7%8E%AF%E6%9E%84%E5%BB%BA%E6%95%99%E7%A8%8B)   标签 将会每日构建(通过Reopen的方式, 因此如果构建失败Issues没有Closed 将终止).  

```diff 
+ 友情提示:
- 7.1 选 jumkey 98% 编译失败, 不用尝试了.
- 只有 DS3615xs 和 DS918+ 支持 6.2.4 版本.
- DS918+ 没有7.1.1, 7.1.1-42951 现在为beta版本(pocopico).
- 有关map参数：SataPortMap=有几位就表示有几个控制器。DiskIdxMap=按顺序从左到右每两位数(16进制)为一个控制器的盘序数值.
- - 因此 DiskIdxMap 的位数应该是 SataPortMap 的2倍。eg: 1,00  22,0002  222,000204.
```

方式二：   
fork 本项目 通过 Actions 填写相关参数进行构建。



#### title:
标题请以 custom 开头（不区分大小写），且不要包含'(单引号),"(双引号) 等转义字符。
- eg:
  - custom 918
  - Custom test
  - CUSTOM Ing 定制
  
#### body:
内容 以json格式编写 ( 切记符号为英文符号，[json check](https://json-online.com/check/))

参数      | 必选  |     默认值     | 说明  
----------|------|----------------|---------
platform  | √    |"DS918+"        | 选择你需要编译的型号. "DS3615xs", "DS3617xs", "DS918+", "DS920+", "DS3622xs+"  
version   | √    |"7.1.0-42661"   | 选择你需要编译的版本. "7.1.1-42951", "7.1.0-42661", "7.0.1-42218", "6.2.4-25556"  
map       | ×    |-               | 控制器盘数(SataPortMap)和盘序(DiskIdxMap)两个字段, 并以","间隔. eg: "0, 10"  
dtb       | ×    |-               | dtb文件下载URL(support ext: .dts,.dtb,.tar.gz,.zip) [#47](https://github.com/wjz304/Redpill_CustomBuild/issues/47)
sn        | ×    |-               | 序列号. 默认根据型号随机生成. eg: "1980PDN002189" 
mac       | ×    |-               | MAC地址. 多个请以 "," 间隔. 默认根据型号随机生成. eg: "001132888A95, 001132888A96"  
usb       | ×    |"0x0001, 0x46f4"| 设备识别码（pid）和供应商ID（vid）[格式: pid, vid]. 默认无.  eg: "0xa4a5, 0x0525"  
ext       | ×    |-               | 多个请以 "," 间隔. 可选项参考: [[rp-ext](https://raw.githubusercontent.com/pocopico/rp-ext/main/exts)]. eg: "r8125, tg3"  
exp       | ×    |"pocopico"      | 编译依赖的基础库. "pocopico", "jumkey" (大佬的抉择，7.1 优先选 pocopico, 7.0-jun 优先选 jumkey)
jun       | ×    |"0"             | 仅7.0.1-42218 版本可以选择jun模式，jun模式 支持 7.01~7.1u3 的 DSM。

- eg:
  - {"platform":"DS3622xs+", "version":"7.0.1-42218", "jun":"1", "ext":"r8125, tg3"}  
  - {"platform":"DS3622xs+", "map":"1, 10", "usb":"0xa4a5, 0x0525"}  
  - {"platform":"DS3622xs+", "version":"7.1.0-42661", "sn":"1980PDN002189", "mac":"001132888A95", "ext":"r8125"}  
  - {"platform":"DS3622xs+", "version":"7.0.1-42218", "jun":"1", "mac":"001132888A95, 001132888A96", "ext":"r8125, tg3"}  
  - {"platform":"DS920+", "version":"7.0.1-42218", "dtb": "https://github.com/wjz304/Redpill_CustomBuild/files/9235785/ds920p.zip", "ext":"r8125"}  
  - {  
      "platform":"DS3622xs+",  
      "version":"7.0.1-42218",  
      "jun":"1",  
      "exp": "jumkey",  
      "mac":"001132888A95, 001132888A96, 001132888A97",  
      "ext":"r8125, r8168, e1000e, igb, vmxnet3, ixgbe"  
    }  
  
## 写在这里
1. pocopico 还是 jumkey 我抉择不了就让你们自己决定把。
2. ext 当前使用 pocopico 库。
3. 驱动默认集成 acpid, misc, virtio, dtb-static(only DS920+)。
4. SN&MAC算号使用 pocopico 的脚本。
5. 最新支持body换行和自动去除控制字符，但是json格式错误无法处理，


## 鸣谢
https://github.com/RedPill-TTG/redpill-load  
https://github.com/jumkey/redpill-load  
https://github.com/pocopico/redpill-load  
https://github.com/Online24Hours/Redpill_Build  

