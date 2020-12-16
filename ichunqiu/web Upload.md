# Upload

题目内容：来来来，都是套路，贼简单。

打开页面显示：Hi,CTFer!u should be a fast man:)

- 查看页面源码显示：
```html
</br>Hi,CTFer!u should be a fast man:)<!-- Please post the ichunqiu what you find -->
```
- 通过burp suite抓包发现http头部有flag信息，内容是base64加密。解密后并非是flag，结合Please post the ichunqiu what you find提示，应该是把解密的信息赋值给ichunqiu参数并通过post方式提交。但是每次打开页面flag信息都不一样，因此需要写脚本完成。
```python
import base64,requests

def main():
    url = "http://293ff781dd0e48df9281ce5c3c31453af01a7caca9d24df0.changame.ichunqiu.com"
    a = requests.session()
    b = a.get(url)
    key1 = b.headers["flag"]
    print(key1)
    c = base64.b64decode(key1)
    d = str(c).split(':')
    key = base64.b64decode(d[1])
    print(key)
    body = {"ichunqiu":key}
    f = a.post(url,data=body)
    print(f.text)
if __name__ == '__main__':
    main()
```
- 成功获得路径信息。打开地址后发现需要登录和验证码。通过dirmap扫描这个路径未发现有用信息。实际有.svn目录，但没有.svn/entries。但有.svn/wc.db，打开后有username信息，给了一个字符串HEL1OW10rDEvery0n3，要求加密后得出的md5即是用户名。
mac上通过命令
```
md5 -s HEL1OW10rDEvery0n3
```
获得用户名8638d5263ab0d3face193725c23ce095

- 验证码通过脚本获取
```python
import hashlib
def md5(s):
    return hashlib.md5(str(s).encode('utf-8')).hexdigest()
def main(s):
    for i in range(1,99999999):
        if md5(i)[0:6]  == str(s):
            print(i)
            exit(0)
if __name__ == '__main__':
    main("7e4675")
```

- password没有任何提示信息，随意输入1234竟然通过了，看来密码并没有加入判断。
- 获得下一个路径后发现是一个上传页面，提示上传jpg。上传一个php果然不行，通过burpsuite修改Content-Type为image/jpg，并把文件后者改成.pht即通过。


