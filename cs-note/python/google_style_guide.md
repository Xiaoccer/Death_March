# Google Python Style Guide
## 总结

## pylint工具

使用pylint进行代码检查。

## Import

在导入整个模块时，可以根据情况用以下方法：

```
import x # 导入整个x模块
from x import y # 导入x中的y
from x import y as z # 当可能有多个导入模块重名时，可以给导入的模块取一个别名z
from x.y import z # 当需要导入自己开发的一些模块的时候
```

## Packages

导入模块时使用完整的路径名

