# BlockingHome
**一个临时的主页**

我会在这个主页讨论关于组件化OS的个人理解，以及一些具体实践

## 组件化设计

<img src="https://github.com/guoweikang/BlockingHome/assets/18571063/84522c69-37d7-40e2-b0ca-8613b32fb843" width="500" height="300">

使用积木比喻组件化的设计是非常形象的 任何一个独立的组件应该具备或者遵守下面的原则: 
 - 功能是 **独立 清晰**的
 - 对外接口 **稳定 明确**的
 - 外部依赖的组件也应该满足上述要求

拥有了组件，是否可以直接从组件拼装成为一个OS?

![1711603979483](https://github.com/guoweikang/BlockingHome/assets/18571063/fea1ceb5-f179-4363-9bb9-e98472d81402)

造成这个问题的主要原因在于: 
 - 如何组装成OS是困难的，OS是一个系统工程，方案的设计和模型搭建需要专业的人员设计和实现
 - 组件之间的接口适配(契合)是难以约束的，也不应该互相约束，需要专门的封装适配

因此，希望通过组件化构建出**好看 好用**的OS,需要一些顶层的设计,事实上，也已经有了一些具体实现:
 - ArceOS: 一个组件化封装设计实现良好的Unikernel
 - arceos-hypervisor:  一个正在做组件化实现的虚拟化实现
 - starry: 一个宏内核的组件化实现
 - ...: 更多优秀的实现案例

![1711604578911](https://github.com/guoweikang/BlockingHome/assets/18571063/185d181a-db7a-431e-bd41-eda63e4e4e37)

## 重构目标
我们已经看到，现在有很多组件化的优秀实践，但是目前这些OS在实现过程中，每个实现都是一个独立的仓库，各个组件都在自己的仓库中维护，因此会存在几个问题: 
 - 组件是否真的符合组件设计原则？是否足够通用？是否自己当前产品耦合？
 - 相同组件无法做到独立迭代，也无法做到产品之间共用

因此我们这次重构目标为: 
 - 梳理通用组件，并把它独立出去，各个OS通过外部仓库方式引用
 - 梳理特殊组件，哪些组件是产品所特有的功能，如果组件本身符合设计原则，也可以独立出去，作为特殊产品的组件

## 改造的OS清单
下表列出了进行改造的OS实现的仓库地址
| OS | Extra modules | Enabled features | Description |
|-|-|-|-|
| [ArceOS](https://github.com/guoweikang/arceos/tree/guoweikang/blocking-unikernel) | | | 从ArceOS Fork过来的仓库 一个unikernel的实现 |
| [ArceOS-hyp](https://github.com/guoweikang/arceos/tree/guoweikang/blocking-hyp) | | | 从ArceOS-hyp Fork过来的仓库 一个虚拟化的实现 |
| [Arceos-monolithic](https://github.com/guoweikang/arceos/tree/guoweikang/blocking-mon) | | | 从Arceos-monolithic Fork过来的仓库 一个宏内核的实现 |

我们将对上述三个仓库同步进行组件化的改造验证

## 组件清单
### 通用组件
#### OS
#### 驱动
| App | Extra modules | Enabled features | Description |
|-|-|-|-|
| [arm_gic](apps/helloworld/) | | | 支持arm-gic v2 v3的驱动实现  |


### 特殊组件






