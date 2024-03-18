===============
My Org learning
===============


.. contents::



1 head 1 :test:
--------

this is head 1 content.
another line.

1.1 head 1-1 :happy:
~~~~~~~~~~~~

head 1-1 content is here.

2 head 2
--------

head 2 content.

2.1 head 2-1
~~~~~~~~~~~~

random content.

3 questions
-----------

3.1 TODO what is a "sparse tree"?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

3.2 TODO agenda thing.
~~~~~~~~~~~~~~~~~~~~~~

4 ideas
-------

也许键盘需要一些有接触感应的按键，这样就可以知道手指是不是放对位置了，因为有的时候，手指放的位置其实不对，这样就可以少看几次键盘了。虽然键盘有一个小小的凸起可以做到这个，但是是不是这个东西还有更多的用法？

5 improvement
-------------

5.1 DONE emacs的那啥，输入法问题，在evil的插入模式自动进入之前插入模式的输入法，而在normal模式只使用英文的输入法。
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

就是在插入模式下的输入法模式在切换模式的时候会被记录下来，再次进入的时候恢复，而在其它模式的时候只使用英文输入法？

5.2 TODO emacs的导出可以有一个css文件来格式化导出的html，让导出更好看。
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

不少内容都是搜索"css for org"搜出来的。
`hugo <https://gohugo.io/>`_
`Is there a collection of CSS styles for Org exports? What are your favorites? <https://www.reddit.com/r/emacs/comments/3pvbag/is_there_a_collection_of_css_styles_for_org/>`_ 这个贴子里边有一个
``#+HTML_HEAD: <link rel="stylesheet" type="text/css" href="https://orgmode.org/worg/style/worg.css"/>``
这个好看，但是这个网页不能自动适配不同的屏幕，是不是改一改就可以了。

5.2.1 github
^^^^^^^^^^^^

`orgcss <https://github.com/gongzhitaao/orgcss?tab=readme-ov-file#caveats>`_
`org-html-themes <https://github.com/fniessen/org-html-themes>`_
我比较想要的格式是，目录在左边，并且可以收起来，想看的时候在展开的那种，这样比较适合手机看。
判断的逻辑是屏幕的长宽比，如果是横着的那种屏幕，那就直接显示目录。如果是竖着的目录，比如手机，那就在左上角显示一个目录图标，点击后再显示目录。具体参考arch-wiki。`Arch Wiki Style <https://wiki.archlinux.org/title/Help:Style>`_

6 expand
--------

6.1 org-roam
~~~~~~~~~~~~

7 疑问
------

7.1 怎么快捷的改变title的等级？
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

7.2 DONE 怎么编辑已经写好的链接？
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

c-c c-l就可以了哦，很好。

7.3 DONE 怎么在minibuffer粘贴？？
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

c-y就可以粘贴了，棒棒。

7.4 DONE 在org里边怎么打开一个link？
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

c-c c-o

7.5 TODO refile是干嘛用的？？
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`https://blog.aaronbieber.com/2017/03/19/organizing-notes-with-refile.html <https://blog.aaronbieber.com/2017/03/19/organizing-notes-with-refile.html>`_
这个文章说了下refile的用法，不过还需要一些前题知识比如agenda怎么使用，先暂缓吧。

8 refile test
-------------

abc abc
