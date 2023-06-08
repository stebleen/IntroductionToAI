# Inter oneAPI——通过DPC++实现异构计算
## 1.oneAPI介绍
Intel oneAPI 是一个跨行业、开放、基于标准的统一的编程模型，它为跨 CPU、GPU、FPGA、专用加速器的开发者提供统一的体验，包含两个组成部分∶ 一项行业计划和一款英特尔beta 产品。

oneAPI 开放规范基于行业标准和现有开发者编程模型，广泛适用于不同架构和来自不同供应商的硬件。oneAPI 行业计划鼓励生态系统内基于oneAPI规范的合作以及兼容 oneAPI的实践。

英特尔 oneAPI 产品是英特尔基于oneAPI 的实现，它包括了 oneAPI 标准组件如直接编程工具（Data Parallel C++）、含有一系列性能库的基于 API 的编程工具，以及先进的分析、调试工具等组件。开发人员从现在开始就可以在英特尔 DevCloud for oneAPI 上对基于多种英特尔架构（包括英特尔至强可扩展处理器、带集成显卡的英特尔酷睿处理器、英特尔 FPGA 如英特尔 Arria、Stratix 等）的代码和应用进行测试。

## 2.DPC++简介
DPC++是Data Parallel C++（数据并行C++）的首字母缩写，它是Intel为了将SYCL引入LLVM和oneAPI所开发的开源项目。SYCL是为了提高各种加速设备上的编程效率而开发的一种高级别的编程模型，简单来说它是一种跨平台的抽象层，用户不需要关心底层的加速器具体是什么，按照标准编写统一的代码就可以在各种平台上运行。可以说SYCL大大提高了编写异构计算代码的可移植性和编程效率，已经成为了异构计算的行业标准。值得一提的是SYCL并不是由多个单词的首字母的缩写。DPC++正是建立在SYCL和现代C++语言之上，具体来说是建立在C++17标准之上的。

### 背景————数据并行编程
数据并行编程既可以被描述为一种思维方式，也可以被描述为一种编程方式。 数据由一组并行的处理单元进行操作。 每个处理单元都是能够对数据进行计算的硬件设备。这些处理单元可能存在于单个设备上，也可能存在于我们计算机系统中的多个设备上。 我们可以指定代码以内核的形式处理我们的数据。 内核是数据并行编程中一个重要的概念，它的功能是让设备上的处理单元执行计算。这个术语在SYCL、OpenCL、CUDA 和 DPC++都有使用到。

### 背景————异构系统
异构系统是包含多种类型的计算设备的任何系统。 例如，同时具有CPU和GPU的系统就是异构系统。现在已经有很多中这样的计算设备了，包括 CPU、GPU、FPGA、DSP、ASIC和AI 芯片。异构系统的出现带来了一个很大的挑战，就是刚刚提到的这些设备，每一种都具有不同的架构，也具有不同的特性，这就导致对每个设备有不同编程和优化需求，而DPC++开发一个动机就是帮助解决这样的挑战。

