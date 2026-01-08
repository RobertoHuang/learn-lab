使用UV来进行环境安装

UV是一个Rust编写的、速度极快的Python包和项目管理器



# 安装UV

参考: https://docs.astral.sh/uv/getting-started/installation/

推荐安装方式

```shell
curl -LsSf https://astral.sh/uv/install.sh | sh
```

启用uv自动补全

```
echo 'eval "$(uv generate-shell-completion zsh)"' >> ~/.zshrc
```

启用uvx自动补全

```shell
echo 'eval "$(uvx --generate-shell-completion zsh)"' >> ~/.zshrc
```



# 初始化项目

- 使用uv创建一个新的项目

  ```shell
  uv init hello-world
  cd hello-world
  ```

- 或者也可以在工作目录中初始化项目

  ```shell
  uv init .
  ```



生成的项目文件结构如下

```
├── .gitignore
├── .python-version
├── README.md
├── main.py
└── pyproject.toml
```

# 安装Python

- 安装指定版本python

  ```shell
  uv install python 3.12
  ```

- 列出所有可用的python

  ```shell
  uv python list
  ```

- 更新python小版本

  ```shell
  uv python upgrade 3.12
  ```

  注意: 如果虚拟环境时在升级之前创建的，则它将继续使用旧的python版本。要启用升级必须重新创建虚拟环境

- 删除指定python版本

  ```shell
  uv uninstall python 3.12
  ```

# 虚拟环境管理

- 创建虚拟环境

  ```shell
  # 创建名为.venv的虚拟环境(默认名称)
  uv venv
  
  # 指定虚拟环境名称
  uv venv changx-env
  
  # 创建虚拟环境时指定使用python版本
  uv venv --python 3.11
  ```

- 激活虚拟环境

  ```shell
  source .venv/bin/activate
  ```

  使用uv时无需激活虚拟环境，uv会在工作目录或其任何父目录中查找虚拟环境名为`.venv`的虚拟环境

- 取消激活的虚拟环境

  ```
  deactivate
  ```

  注意，只有运行过激活脚本`deactivate`命令才会存在

- 删除虚拟环境

  ```shell
  rm -rf .venv
  ```



# 基本概念

UV的核心功能

- 包安装: 替代`pip install`
- 虚拟环境管理: 替代`python -m venv`
- 依赖解析: 替代`pip-tools`
- 项目管理: 类似`poetry`和`pipenv`的功能
- Python版本管理: 内置Python版本发现和管理

