---
layout: post
title: "js对象遵守规则"
date: 2016-06-15 16:57:10 +0800
comments: true
categories: 
---


<!-- ``` -->
	•	不要使用new Number()、new Boolean()、new String()创建包装对象； 
	•	用parseInt()或parseFloat()来转换任意类型到number； 
	•	用String()来转换任意类型到string，或者直接调用某个对象的toString()方法； 
	•	通常不必把任意类型转换为boolean再判断，因为可以直接写if (myVar) {...}； 
	•	typeof操作符可以判断出number、boolean、string、function和undefined； 
	•	判断Array要使用Array.isArray(arr)； 
	•	判断null请使用myVar === null； 
	•	判断某个全局变量是否存在用typeof window.myVar === 'undefined'； 
	•	函数内部判断某个变量是否存在用typeof myVar === 'undefined'。
	•   null和undefined 没有toString()方法
	
<!-- ``` -->

