---
title: python 装饰模式
date: 2016-12-12 11:04:09
tags:
---

* 直接上代码


* 不需要编写wrapper.__name__ = func.__name__这样的代码，Python内置的functools.wraps就是
干这个事的，所以，一个完整的decorator的写法如下：

def log(func):
	
	@functools.wraps(func)
	
	def wrapper(*args,**kw):
	
		print('call %s():' % func.__name__)
		
		return func(*args, **kw)
		
	return wrapper


def log(text):

	def decorator(func):
	
		@functools.wraps(func)
		
		def wrapper(*args, **kw):
		
			print('%s %s()' %(text, func.__name__))
			
			return func(*args, **kw)
			
		return wrapper
		
	return decorator
<!-- ``` -->

 * [reference](http://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/0014318435599930270c0381a3b44db991cd6d858064ac0000)

