## vscode一些设置

- word warp：自动换行
- level：整体放大缩小，或者：

  - ctrl+加号：放大
  - ctrl+减号：缩小
- ctrl+shift+p：进入命令行
- 工作区settings设置代理：在.vscode/settings.json下：
  ```json
  {
      "terminal.integrated.env.windows": {
          "HTTP_PROXY": "http://127.0.0.1:xxxx",
          "HTTPS_PROXY": "http://127.0.0.1:xxxx"
      }
  }
  ```
  方便在vscode中使用git
