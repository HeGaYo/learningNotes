cobbler source code Reading
-------
**Makefile**
```
make install

build:
	python setup.py build -f

install: build
	python setup.py install --root $(DESTDIR) -f
```
-----
**cobbler/cobbler/cli.py**

命令行执行cobbler

* main(): 主函数 入口

* run(): remote.login object_type object_action direct_action

* object_command(): 判断参数 执行操作

-----
