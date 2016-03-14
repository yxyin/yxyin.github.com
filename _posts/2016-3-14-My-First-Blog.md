---
layout: post
title: 我的第一篇blog
tags: 性能测试
categories: 性能测试
---

## 记录工作，学习和生活当中的点点滴滴 ##

不知不觉间，研究生毕业已快三年。 从事**性能测试**的工作也已有三年，这其中既有辛酸和苦闷，又有成就与收获。 适逢公司裁员，压力倍增，回顾过去的三年，竟不知该从何说起。 这也是我下决心开始写技术博客的一个原因。

前两天偶遇了静态blog生成工具jekyll，试了一下感觉很方便好用，以后会经常更新blog。

下面是对一些快捷健的标注，之后会对粘贴代码做一个实验
### Built exclusively for Markdown ###
**MarkdownPad** is a full-featured Markdown editor for Windows.
Enjoy first-class Markdown support with easy access to  Markdown syntax and convenient keyboard shortcuts.

Give them a try:##  ##

- **Bold** (`Ctrl+B`) and *Italic* (`Ctrl+I`)
- Quotes (`Ctrl+Q`)
- Code blocks (`Ctrl+K`)
- Headings 1, 2, 3 (`Ctrl+1`, `Ctrl+2`, `Ctrl+3`)
- Lists (`Ctrl+U` and `Ctrl+Shift+O`)

### Java Code test ###

~~~java

//Author: Yunxin Yin

public class Hanio {
	
	public static void hanio(int n, char one, char two, char three) {
		if(n==1) {
			System.out.println("Move from " + one + " to " + three);
		}
		else {
			hanio(n-1, one, three, two);
			System.out.println("Move from " + one + " to " + three);
			hanio(n-1, two, one, three);
		}
	}
	

	public static void main(String[] args) {
		//Add commit again
		//Test at home
		int n = 3;
		hanio(n, 'A', 'B', 'C');
	}

}

~~~
