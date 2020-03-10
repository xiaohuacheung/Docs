# 说明

## 配置mkdoc环境和PDF插件
 > yum install python
 >
 > alias pip='/usr/bin/pip-3.6' 
 >
 > alias python='/usr/bin/python3.6' 
 >
 > pip install mkdocs
 >
 > pip install git+https://github.com/orzih/mkdocs-with-pdf

## Theme
缺省支持的theme有：readthedocs 和 mkdocs ，其它的 theme需要单独安装
1.  theme: material
    >
    > pip install mkdocs-material
    >
    安装完成后支持theme标签取值 material
2.  theme: mkdocs-windmill
    >
    >pip install mkdocs-windmill
    >
    安装完成后支持theme标签取值 windmill
3.  theme: mkdocs-bootstrap  (不好看)
    >
    >pip install mkdocs-bootstrap
    >
    安装完成后支持theme标签取值 bootstrap
4.  theme: mkdocs-bootstrap4
    >
    >pip install mkdocs-bootstrap4
    >
    安装完成后支持theme标签取值 bootstrap4
5.  theme: mkdocs-bootswatch
    >
    >pip install mkdocs-bootswatch
    >
    安装完成后支持theme标签取值 cerulean cosmo cyborg darkly flatly journal litera lumen lux materia minty pulse sandstone simplex slate solar spacelab superhero united yeti
6.  theme: mkdocs-ivory
    >
    >pip install mkdocs-ivory
    >
    安装完成后支持theme标签取值 ivory
 
## PDF插件
安装完成PDF插件后，可以在yml文件中添加plugins配置，直接生成pdf文件以供下载
 >
 >pip install git+https://github.com/orzih/mkdocs-with-pdf
 >
安葬后在yml文件中添加下面的内容
 
     plugins: 
       - search
       - with-pdf

## 生成文档

 >git clone https://github.com/xiaohuacheung/Docs.git
 >cd Docs
 >./build.sh
如果不使用build.sh 脚本，可以直接命令行依次执行下面的内容直接查看其中的一个文档

       cd PbcDoc/Ecmp
       mkdir docs site
       mkdocs build --clean
       mkdocs serve -a localhost:80
       firefox -kiosk http://localhost


========



Install the plugin:

pip install mkdocs-nav-enhancements
Add the plugin to your mkdocs.yml MkDocs configuration file:

plugins:
  - mkdocs-nav-enhancements
 
 
 




