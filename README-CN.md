## llmv dfg

## env

+ [ubuntu 12.04.5](http://mirrors.163.com/ubuntu-releases/12.04.5/ubuntu-12.04.5-server-amd64.iso)
  + 安装完成之后，替换镜像源 vi /etc/apt/sources.list，直接 :%s/us.archive.ubuntu.com/mirrors.163.com/g
  + `apt-get update` & `apt-get dist-upgrade`
  + nano /etc/apt/sources.list ， 注释掉 security 相关的几行镜像源
  + 安装 openssh-server `apt-get install openssh-server`
  + `ip a` 查看IP，然后采用 xshell 连接虚拟机

## LLVM + Clang

+ 安装 gcc `sudo apt-get install gcc g++ make`
+ 下载 [llmv 3.4.1](https://releases.llvm.org/3.4.1/llvm-3.4.1.src.tar.gz)
+ tar 解压，重命名为 llvm
+ 下载 [clang 3.4.1](https://releases.llvm.org/3.4.1/cfe-3.4.1.src.tar.gz) 解压，重命名，放到 llvm/tools/clang
+ 下载 [compiler-rt 3.4.1](https://releases.llvm.org/3.4/compiler-rt-3.4.src.tar.gz) 解压，重命名，放到 llvm/projects/compiler-rt
+ 切换到 build 目录，执行 `../llvm/configure  --disable-optmized`
+ `make -j4` or `make -j8` 编译 (看你的机器 CPU 核心数量)
+ 机器内存，稍微搞大一点，否则 link 的时候会 OOM
+ 编译完之后，执行一波 `echo $?` 看是否 = 0 ，表示是否成功

## DFGenTool

+ clone code from [DFGenTool](https://github.com/misc-research/DFGenTool) into build/lib/Transforms/DFGenTool
+ 切换到 build/lib/Transforms 目录，修改 Makefile，在 ObjCARC 加 DFGenTool，然后执行 make
+ 其他步骤，参考 [README](./Readme.md) 里面的clang路径和module路径不对，需要自己找
