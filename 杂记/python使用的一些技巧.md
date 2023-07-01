### 使用\_\_call__()为类绑定回调函数

来源：PatchTST中自监督预训练中Learner类的写法

```python
class Learner(GetAttr):

    def __init__(self, dls, model,
                        loss_func=None,
                        lr=1e-3,
                        cbs=None,
                        metrics=None,
                        opt_func=Adam,
                        **kwargs):
                
        self.model, self.dls, self.loss_func, self.lr = model, dls, loss_func, lr
        self.opt_func = opt_func
        #self.opt = self.opt_func(self.model.parameters(), self.lr) 
        self.set_opt()
        
        self.metrics = metrics
        self.n_inp  = 2
        # self.n_inp = self.dls.train.dataset.n_inp if self.dls else 0
        # Initialize callbacks                 
        if cbs and not isinstance(cbs, List): cbs = [cbs]    
        self.initialize_callbacks(cbs)        
        # Indicator of running lr_finder
        self.run_finder = False
        
    def __call__(self, name):        
    	for cb in self.cbs: 
            attr = getattr(cb, name)
            if attr is not None: attr()
            
    def fit(self, n_epochs, lr=None, cbs=None, do_valid=True):
        " fit the model "
        self.n_epochs = n_epochs
        if not self.dls.valid: do_valid = False
        if cbs: self.add_callbacks(cbs)
        if lr: self.opt = self.opt_func(self.model.parameters(), lr)  # Adam

        self('before_fit')  #
        try:
            for self.epoch in range(n_epochs):            
                self('before_epoch')                     
                self.one_epoch(train=True)            
                # if self.dls.valid:                    
                if do_valid: self.one_epoch(train=False)                
                self('after_epoch')        
        except KeyboardInterrupt: pass 
        self('after_fit')
```

### globals()的作用

在Python中，`globals()`是一个内置函数，用于返回当前全局作用域中的所有全局变量和它们的值的字典。它返回一个表示全局命名空间的字典，其中键是变量名，值是相应的变量值。

`globals()`函数的主要作用是允许您在任何位置访问和操作全局变量。您可以通过将其存储在一个变量中，并使用该变量进行读取、写入或删除全局变量。这对于需要动态访问全局变量的情况非常有用，尤其是在函数内部或嵌套作用域中。

以下是一些示例代码，展示了如何使用`globals()`函数：

```python
x = 10

def print_global_variables():
    global_vars = globals()
    for var_name, var_value in global_vars.items():
        print(f'{var_name}: {var_value}')

print_global_variables()
# 输出：
# x: 10

def update_global_variable():
    global_vars = globals()
    if 'x' in global_vars:
        global_vars['x'] = 20

update_global_variable()
print(x)  # 输出：20
```

请注意，在修改全局变量时，如果您在函数内部使用`global`关键字声明了一个变量，那么在函数内部将会创建一个局部变量，而不是修改全局变量。因此，`globals()`函数提供了一种绕过此限制的方法，使您能够直接访问和修改全局变量。
