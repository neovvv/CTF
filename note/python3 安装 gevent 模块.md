# MacOS python3 安装 gevent 模块

```bash
ERROR: Command errored out with exit status 1: /Applications/Xcode.app/Contents/Developer/usr/bin/python3 -u -c 'import sys, setuptools, tokenize; sys.argv[0] = '"'"'/private/tmp/pip-install-d7edx1ek/greenlet/setup.py'"'"'; __file__='"'"'/private/tmp/pip-install-d7edx1ek/greenlet/setup.py'"'"';f=getattr(tokenize, '"'"'open'"'"', open)(__file__);code=f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' install --record /private/tmp/pip-record-sr9i1xr3/install-record.txt --single-version-externally-managed --compile --install-headers /Library/Python/3.8/include/greenlet Check the logs for full command output.

```

## 产生原因

MAC OS 的 Xcode 从 5.1 起给编译器规定对于未知参数传入视为 error，我们需要使用 ARCHFLAGS 将该 error 降级为 warning。

## 解决办法
```bash
sudo ARCHFLAGS=-Wno-error=unused-command-line-argument-hard-error-in-future pip3 install gevent
```