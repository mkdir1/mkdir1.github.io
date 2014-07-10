---
layout: post
title: "Markdown转html和pdf"
date: 2014-07-10 17:59:21 +0800
comments: true
categories: Tools

---

### Markdown转html和pdf

这个功能很实用，可以在网上完成．但对于本地，则也有几个不错的工具选择

---

####之前的解决方案

可以在这几个网址上完成转换:

- 1 [马克飞象](http://maxiang.info/),这个很方便，可以同步evernote，b也有不错的界面，是目前我最看好的一个．但唯一不爽的是保存的pdf中竟然有它的logo这个真是要命

- 2 [statedit](https://stackedit.io/),这个也不错，和前者很像．应该大部分这类网站都是这个风格，在没有搭建好本地的转换的时候，本人一直是在这上面完成pdf转换的，想来真是折腾啊
    
- 3 再一个就是linux下的retext了，这是个简单的免费工具，文本操作，对于vim程序员确实使用不爽，唯一的用处就是预览和修改用

- 4 还好，linux下面有一个markdown的命令，使用也简单，也`sudo apt-get isntall markdwon`就行.不过令人不爽的是，html乱码，对中文支持不够，看了官网上的，好像还是2004年的更新，所以一定有我这样的志士仁人受不了

---
#####现在的解决方案

程序员的原则就是大道至简，其实就是方便，通俗点就是懒惰，怎么能忍受如此多的工具换来换去的，那岂不是要疯，最好是一个命令就搞定，生成了pdf, txt, html, md等所有格式，如果要用，就直接里面找．

首先安装`sudo apt-get install pandoc`，再看下它的方法，使用也很简单

**语法如下**

    pandoc -h
    pandoc [OPTIONS] [FILES]
    Input formats:  native, markdown, markdown+lhs, rst, rst+lhs, html, latex, latex+lhs
    Output formats:  native, html, html+lhs, s5, docbook, opendocument, odt, latex, latex+lhs, context, texinfo, man, markdown, markdown+lhs, plain, rst, rst+lhs, mediawiki, rtf
    Options:
      -f FORMAT, -r FORMAT  --from=FORMAT, --read=FORMAT                    
      -t FORMAT, -w FORMAT  --to=FORMAT, --write=FORMAT                     
      -s                    --standalone                                    
      -o FILENAME           --output=FILENAME                               
      -p                    --preserve-tabs                                 
                            --tab-stop=TABSTOP                              
                            --strict                                        
                            --reference-links                               
      -R                    --parse-raw                                     
      -S                    --smart                                         
      -m[URL]               --latexmathml[=URL], --asciimathml[=URL]        
                            --mathml[=URL]                                  
                            --mimetex[=URL]                                 
                            --jsmath[=URL]                                  
                            --gladtex                                       
      -i                    --incremental                                   
                            --xetex                                         
      -N                    --number-sections                               
                            --no-wrap                                       
                            --sanitize-html                                 
                            --email-obfuscation=none|javascript|references  
                            --id-prefix=STRING                              
                            --indented-code-classes=STRING                  
                            --toc, --table-of-contents                      
                            --base-header-level=LEVEL                       
                            --template=FILENAME                             
      -V FILENAME           --variable=FILENAME                             
      -c URL                --css=URL                                       
      -H FILENAME           --include-in-header=FILENAME                    
      -B FILENAME           --include-before-body=FILENAME                  
      -A FILENAME           --include-after-body=FILENAME                   
      -C FILENAME           --custom-header=FILENAME                        
      -T STRING             --title-prefix=STRING                           
                            --reference-odt=FILENAME                        
      -D FORMAT             --print-default-template=FORMAT                 
                            --data-dir=DIRECTORY                            
                            --dump-args                                     
                            --ignore-args                                   
      -v                    --version                                       
      -h                    --help
支持格式中，比较有用的有**markdown, html, latex, rtf, odt

####使用

```
pandoc -f markdown -t html -o example.html example.md
pandoc --ascii example.md -o example.html
    
```
加--ascii后html不会乱码

####转为pdf 
这个历程真是坑，转为pdf的软件何其多，当初很2的选择了xhtml2pdf.这个软件我至今还没安装好，依赖包好多，PIL, Reporlab．最后安装好了，还是出问题．当时的想法就是换一个软件．终于有一个神器出现了

    sudo apt-get install unoconv

使用也很方便，`unoconv -f pdf demo.html`

为什么说**unoconv**是神器了，用了才知道它支持好多格式，常用的几乎包含了．

####写个Makefile就好了

    MD = pandoc
    MDFLAGS = --ascii
    H2P = unoconv
    H2PFLAGS = -f pdf 
    SOURCES := $(wildcard *.md)
    OBJECTS := $(patsubst %.md, %.html, $(wildcard *.md))
    OBJECTS_PDF := $(patsubst %.md, %.pdf, $(wildcard *.md))
    all: build
    build: html pdf
    pdf: $(OBJECTS_PDF)
    html: $(OBJECTS)
    $(OBJECTS_PDF): %.pdf: %.html
    	$(H2P) $(H2PFLAGS) $< 
    $(OBJECTS): %.html: %.md
    	$(MD) $(MDFLAGS) -o $@ $<
    clean:
    	rm -f $(OBJECTS) *.pdf
这样再直接用就一切ok

####写个Shell一切安好

这里整理一下要点

- 1. 查找匹配后缀名`find * -type f -name '*.md'`，这里如果find后是.则匹配的文件有本目录如，./demo.md，如果用*则如demo.md

- 2.匹配文件名和后缀，如果file="thisfile.md",则${file%.*}表示thisfile, ${file##*.}表示md


**详细代码，我的shell名为tran.sh**

    #!/bin/sh                                                          
    filelist=`find * -type f -name '*.md'`
    for file in $filelist
    do   
        htmlfile=${file%.*}.html
        pandoc --ascii $file -o $htmlfile
        unoconv -f pdf $htmlfile
    done 

最后就放到bin中就搞定了

有的后缀很花样，没办法，把shell中两行改为:
    filelists=`find * -type f -name '*.markdown'`
    for file in $filelist $filelists
Enjoy~
