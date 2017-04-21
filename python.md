# 安装 easy_install / pip
新版的 python 默认会安装 easy_install 和 pip，安装完成后注意将目录添加到 path 里面，就可以直接使用了。

如果需要通过代理下载，可以将代理配置到环境变量
```bash
export http_proxy=http://proxy_url:proxy_port
export https_proxy=http://proxy_url:proxy_port
```
pip 还支持 proxy 选项
```
pip install --proxy=http://proxy_url:proxy_port package
```
# 打包为可执行文件（windows）
* 安装 pyinstaller
```bash
easy_install pyinstaller
```
* 打包
```bash
pyinstaller youpythonfile.py
```
打包为一个文件
```bash
pyinstaller --onefile youpythonfile.py
```
[官方文档](https://pyinstaller.readthedocs.io/en/stable/)
