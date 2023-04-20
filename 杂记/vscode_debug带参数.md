参考：[[zhihu](https://www.zhihu.com/question/50700473)]

```json
{
  // Use IntelliSense to learn about possible attributes.
  // Hover to view descriptions of existing attributes.
  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
  "version": "0.2.0",
  "configurations": [
    {
      "name": "${workspace}/main.py",   
      "type": "python",
      "request": "launch",
      "python": "/home/usrname/anaconda3/envs/envs_name/bin/python",
      "args": [
        "--input_path",
        "~/input_path",
      ],      
      "program": "${file}",
      "console": "integratedTerminal"
      "env": {"PYTHONPATH": "${workspaceFolder}/libs/"}
    }
  ]
}
```

