Ok, if by Portable Python you mean the embeddable zip file that Python.org provides, than this guide solved my problem: [https://michlstechblog.info/blog/python-install-python-with-pip-on-windows-by-the-embeddable-zip-file/](https://michlstechblog.info/blog/python-install-python-with-pip-on-windows-by-the-embeddable-zip-file/)

Here's the text in case it goes offline:

To install Python on Windows download the latest version. In this example Python 3.6.5.

Extract the zip file to an directory, e.g. D:\python3.6.5.

To install pip download the latest version of [get-pip](https://bootstrap.pypa.io/get-pip.py) to the pythons install path and start installation.

```
> d:\> cd /d D:\Python3.6.5 D:\Python3.6.5> python get-pip.py ...
> Installing collected packages: pip, setuptools, wheel Successfully
> installed pip-10.0.1 setuptools-39.2.0 wheel-0.31.1
```

If you are behind a proxy add the –proxy switch

```
D:\Python3.6.5> python get-pip.py --proxy="http://192.168.254.1:8888"
```

Unfortunately in the default configuration you can not load any module installed by pip, pip itself too. Because the sys.path variable just contains Python Zip file and the path to the python directory where the python executable is located.

```
>>> import sys
>>> print(sys.path)
['D:\\Python3.6.5\\python36.zip', 'D:\\Python3.6.5']
>>> import pip
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'pip'
```

Any try to expand the variable by setting a PYTHONPATH variable are ignored. Root cause is that the embeddable zip file installation package contains a file python36._pth which overwrites all other possibilities to set the sys.path variable. sys.path contains all directories where python looks for modules.

To set the sys.path variable open the _pth file an add the following pathes at the and of the file. Replace “D:\Python3.6.5” with your installation directory.

```
D:\Python3.6.5
D:\Python3.6.5\DLLs
D:\Python3.6.5\lib
D:\Python3.6.5\lib\plat-win
D:\Python3.6.5\lib\site-packages
```

Or rename the python36._pth file

```
D:\Python3.6.5> ren python36._pth python36._pth.save
```

and set the PYTHONPATH environment variable for the current user.

```
setx PYTHONPATH "D:\Python3.6.5;D:\Python3.6.5\DLLs;D:\Python3.6.5\lib;D:\Python3.6.5\lib\plat-win;D:\Python3.6.5\lib\site-packages"
```

or for the whole system

```
setx /M PYTHONPATH "D:\Python3.6.5;D:\Python3.6.5\DLLs;D:\Python3.6.5\lib;D:\Python3.6.5\lib\plat-win;D:\Python3.6.5\lib\site-packages"
```

[Share](https://stackoverflow.com/a/55271031 "Short permalink to this answer")

[Improve this answer](https://stackoverflow.com/posts/55271031/edit)

Follow