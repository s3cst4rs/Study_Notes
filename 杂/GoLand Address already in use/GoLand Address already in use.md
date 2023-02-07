在打开 GoLand 的时候，突然出现了 Start Failed，错误是 address already in use bind

大概弹窗是下面这样，我的图没有截，这里用网上的一张图来说明

![image-20230114093824459](./GoLand%20Address%20already%20in%20use.assets/image-20230114093824459.png)

官方给的描述是在启动的时候，会尝试绑定 6942 和 6991 之间的第一个可用端口

正常来说不应该出现全都被占用的情况



后面经过搜索，找到了一个可以的解决方案

管理员权限执行下面的命令即可

```
net stop winnat
net start winnat
```

