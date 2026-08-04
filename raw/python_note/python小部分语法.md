## Python一些技巧

- os.walk用法：

  ```

  def walkFile(file):

      for root, dirs, files in os.walk(file):


          # root 表示当前正在访问的文件夹路径

          # dirs 表示该文件夹下的子目录名list

          # files 表示该文件夹下的文件list


          # 遍历文件

          for f in files:

              print(os.path.join(root, f))


          # 遍历所有的文件夹

          for d in dirs:

              print(os.path.join(root, d))

  ```
- 获取脚本所在目录

  ```

  os.path.split(os.path.realpath(__file__))[0]

  ```
- nohup: nohup指不断地运行，是no hang up的缩写，指不间断，不挂断。运行一个进程的时候，不想让其在你退出账号时关闭，即可用nohup:

  ```

  nohup python my.py >> my.log 2>&1 &

  # 或者

  nohup python my.py >> nohup.out 2>&1 &

  # 或者

  nohup python my.py &  # 这种写法和上面第二种写法等价

  ```
- sklearn全称为**scikit-learn**
- 获取路径

```

import os

# 获取当前文件的绝对路径

current_file_path = os.path.abspath(__file__)


# 获取当前文件所在目录

current_directory = os.path.dirname(current_file_path)


# 写在文件最上面，包含根目录（该文件目录的父目录）

import os

import sys

sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), '..')))

```
