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

