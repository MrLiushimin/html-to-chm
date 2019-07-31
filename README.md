# html-to-chm
wget获取整个网站html,并转化为chm文档(英文网站->使用google翻译转中文)


# 获取整个网站页面
wget -r -p -np -k http://xxx.com/xxx
-r, --recursive（递归） specify recursive download.（指定递归下载）
-k, --convert-links（转换链接） make links in downloaded HTML point to local files.（将下载的HTML页面中的链接转换为相对链接即本地链接）
-p, --page-requisites（页面必需元素） get all images, etc. needed to display HTML page.（下载所有的图片等页面显示所需的内容）
-np, --no-parent（不追溯至父级） don't ascend to the parent directory.
-a<日志文件>：在指定的日志文件中记录资料的执行过程；
 -A<后缀名>：指定要下载文件的后缀名，多个后缀名之间使用逗号进行分隔； 
-b：进行后台的方式运行wget； -B<连接地址>：设置参考的连接地址的基地地址； 
-c：继续执行上次终端的任务；
 -C<标志>：设置服务器数据块功能标志on为激活，off为关闭，默认值为on； 
-d：调试模式运行指令； 
-D<域名列表>：设置顺着的域名列表，域名之间用“，”分隔；
 -e<指令>：作为文件“.wgetrc”中的一部分执行指定的指令；
 -h：显示指令帮助信息； -i<文件>：从指定文件获取要下载的URL地址；
 -l<目录列表>：设置顺着的目录列表，多个目录用“，”分隔； -L：仅顺着关联的连接； 
-r：递归下载方式；
 -nc：文件存在时，下载文件不覆盖原有文件；
 -nv：下载时只显示更新和出错信息，不显示指令的详细执行过程；
 -q：不显示指令执行过程； 
-nh：不查询主机名称； 
-v：显示详细执行过程；

 -V：显示版本信息； 

--passive-ftp：使用被动模式PASV连接FTP服务器；

 --follow-ftp：从HTML文件中下载FTP连接文件。

--------------------- 

# 批量替换掉不需要的内容
## 查看需要替换的内容
grep '<script src="https://ssl.google-analytics.com/urchin.js"' *
<!--<script src="https://ssl.google-analytics.com/urchin.js"
<script src="https://ssl.google-analytics.com/urchin.js"

grep '</script><div id="container">' *
</script>--><div id="container">


grep '</div></form></noscript>' *
</div></form></noscript><!--

grep '              </script>' *
              </script>-->

## 找文件
find . -type f -name "*.html"|xargs grep '</script><div id="container">'

## 替换文件中的内容
find -name '要查找的文件名' | xargs perl -pi -e 's|被替换的字符串|替换后的字符串|g'

find . -type f -name "*.html"| xargs perl -pi -e 's|<script src="https://ssl.google-analytics.com/urchin.js"|<!--<script src="https://ssl.google-analytics.com/urchin.js"|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|</script><div id="container">|</script>--><div id="container">|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|</div></form></noscript>|</div></form></noscript><!--|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|              </script>|              </script>-->|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|href="index.html"|href="../index.html"|g'


# 整理目录,将js、css等文件路径进行处理
find . -type f -name "*.html"| xargs perl -pi -e 's|被替换的字符串|替换后的字符串|g'

find . -type f -name "*.html"| xargs perl -pi -e 's|C.css|../C.css|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|jquery.js|../jquery.js|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|jquery.syntax.js|../jquery.syntax.js|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|yelp.js|../yelp.js|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|yelp-note.png|../yelp-note.png|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|yelp-note-tip.png|../yelp-note-tip.png|g'
find . -type f -name "*.html"| xargs perl -pi -e 's|yelp-note-warning.png|../yelp-note-warning.png|g'

# 将英文翻译成中文(打开网页,使用google翻译,F12复制网页),放到对应的文件夹

# 处理js文件

# 使用Easy CHM将网页转换成chm文档



