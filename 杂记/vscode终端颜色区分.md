参考连接：[[csdn](https://blog.csdn.net/weixin_39065428/article/details/129370830)]

在PythonXY\Lib\site-packages（Anaconda位置为envs/XX/PythonXY/site-packages）中添加sitecustomize.py，内容如下：

```python
import sys
from IPython.core.ultratb import ColorTB
 
sys.excepthook = ColorTB()
```

