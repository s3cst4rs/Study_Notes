# 介绍

最近实现了一下 Golang 版本的 RDI，发现 WBG 已经实现过了，就直接借鉴一下

因为自己有对 RDI 进行其他的修改，就没办法直接拿来用了，在适配的时候发现在 Go 当中调用跟直接调用 C 版本一些差别，这里记录一下



# 差异

在原版的 RDI 中，是通过 Intel 提供了一个函数来获取当前在 PE 文件中的位置

```
__declspec(noinline) ULONG_PTR caller( VOID ) { return (ULONG_PTR)_ReturnAddress(); }
```

而用 GCC 编译的时候是没有这个符号的，需要替换

```
__declspec(noinline) ULONG_PTR caller( VOID ) { return (ULONG_PTR)__builtin_return_address(0); }
```

在 GCC 文档中也能够看到相关的描述 https://gcc.gnu.org/onlinedocs/gcc/Return-Address.html



还有一个目前不确定作用的宏 `MINGW_FORCE_SYS_INTRINS` ，在刚开始编译的时候有重复定义的问题，后续又没有了，但是这个宏又跟这些没有关系，有可能是编译问题，重新编译之后才正常的，具体原因不清楚



对于其他的并没有太大的差别，主要还是 GCC 与 MSVC 的差异造成的一些小问题

# 参考

https://github.com/WBGlIl/go-ReflectiveDLL

https://xz.aliyun.com/t/10143