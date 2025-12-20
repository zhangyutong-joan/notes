## vscode launch.json常用配置：

```
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
 "configurations": [
        {
            "name": "Python: 你想用的环境名1",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "justMyCode": true,
             //环境名对应的python路径
            "python": "/home/你的用户名/anaconda3/bin/python"
        },
        {
            "name": "Python: 你想用的环境名2",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "justMyCode": true,
            "python": "/home/你的用户名/anaconda3/envs/verse/bin/python" 
        }
    ]
}

```
