# mfd

Spotlight 是 OS X 上非常好用的一个桌面搜索工具，mdfind 是Spotlight 的 CLI frontend，
虽然 mdfind 的功能足够强大，但是界面非常不友好，例如，要搜索电脑中2013年的文件大小大于 1MB
的jpg图像文件，需要一个非常复杂的命令。mfd 对mdfind进行封装，提供比较易用的界面


## 用法

```
mfd [options]

  通过指定若干选项来搜索文件系统中被 Spotlight 索引的文件，每个选项之间是逻辑与的关系. 默认将
  搜索文件系统中所有的被索引文件，可以通过 "-o" 选项来约束其只在某个目录中进行搜索.  

  % mfd --content-type com.omnigroup.omnigraffle.graffle --from 2011/11/1 -t '2013-01-01 14:30:24'
  % mfd --query '关键字' --content-type 'com.adobe.pdf'
  % mfd -e mp3 -b10M

options:

  以下选项均支持以一个 "@" 符号开头, 后跟一个文件名，表示此选项的值将从给定的文件中提取:

    • -f, --from
    • -t, --to
    • -F, --from-create
    • -T, --to-create
    • -c, --content-type
    • -k, --kind
    • -b, --biggerthan
    • -s, --smallerthan

    -f, --from from                  e.g. --from 2010/1/1
                                     搜索"文件最后修改时间"等于或晚于指定时间的文件，时间格式为"YYYY-mm-dd HH:MM:SS"
                                     其中可以使用任意非数字字符作为分隔符，也可以只指定日期部分。
                                     另外, -f 选项还支持指定一个数字后跟一个字母的形式来指定时间,
                                     支持的字符包括: S, M, H, d, m, Y，分别表示: 秒, 分, 时,
                                     天, 月, 年, 其中一个月等于 30 天, 一年等于 365 天.
                                     例如, 搜索最近 10 天的文件: -f 10d 
  
    -t, --to to                      搜索"文件最后修改时间"等于或早于指定时间的文件, 格式同"-f"选项
  
    -F, --from-create from           搜索"文件创建时间"等于或晚于指定时间的文件, 格式同"-f"选项
  
    -T, --to-create to               搜索"文件创建时间"等于或早于指定时间的文件, 格式同"-f"选项
  
    -q, --query query                e.g. --query "关键字"
  
    -c, --content-type contenttype   e.g. --contenttype com.omnigroup.omnigraffle.graffle
                                     搜索 "kMDItemContentType" 属性等于指定值的文件，可以不
                                     指定完整的 Content Type，例如 Ruby 脚本的 Content Type
                                     为 "public.ruby-script"，但是可以使用下面的命令所有所有
                                     Ruby 脚本文件：mfd -c ruby
  
    -e, --type file-ext-name         .e.g  -e 'mp3'
                                     ContentType 字符串不便记忆，为了方便使用，本程序将常用的
                                     文件类型的后缀名和 ContentType 字符串建立关联，可以使用本选项
                                     来指定要搜索的文件的后缀名, 可以使用"-l"选项查看所有支持的后
                                     缀名以及关联
  
    -l, --list-types                 ContentType 字符串不便记忆，为了方便使用，本程序将常用的
                                     文件类型的后缀名和 ContentType 字符串建立关联，使用本选项
                                     看所有支持的后缀名以及关联
  
    -k, --kind kind                  e.g. --kind "HTML Document"
                                     "-k"选项是另外一个用来指定文件类型的选项，它使用
                                     "kMDItemKind"属性来搜索文件. 例如, 搜索邮件: "-k 邮件信息"
                                     搜索 Safari 历史记录: "-k 'Safari 历史记录项目'"
  
    -b, --bigger-than size           e.g. --bigger-than 100000
                                     搜索文件大小大于或等于给定值的文件，可以使用 t, g, m, k 等单位,
                                     例如, 搜索大于或等于 1MB 字节的文件："-b 1m"
  
    -s, --smaller-than size          e.g. --smaller-than 100000
                                     搜索文件大小小于或等于给定值的文件，可以使用 t, g, m, k 等单位,
                                     例如, 搜索小于或等于 1GB 字节的文件："-b 1G"
  
        --prop-eq arg_value
                                     e.g. --prop-eq FSSize@diary.txt
                                     不同类型的文件各自都有多种多样的属性，本程序支持的属性比较有限, 若需要
                                     按照其他属性比较，则使用本选项以及下面三个以 "--prop" 
                                     打头的选项。可以通过 OS X 自带的 "mdls" 命令来查看文件的各种属性,
                                     属性名称一般以 "kMDItem" 打头，使用这四个选项时可以只指定 "kMDItem"
                                     后面的部分, 本选项的值的格式为 "property@filename", 例如,
                                     搜索文件大小等于 a.txt 的所有文件：--prop-eq FSSize@./a.txt
  
        --prop-ne arg_value
                                     e.g. --prop-ne FSSize@diary.txt
  
        --prop-le arg_value
                                     e.g. --prop-le FSSize@diary.txt
  
        --prop-ge arg_value
                                     e.g. --prop-ge FSSize@diary.txt
  
    -d, --downloadfrom url           搜索从URL下载的文件
    -n, --name name                  按文件名称搜索, 自动支持模糊匹配, 无需指定通配符
    -0, --null                       Prints an ASCII NUL character after each result path. 
                                     This is useful when used in conjunction with 
                                     xargs -0.
        --live
                                     Causes the mdfind command to provide live-updates to the  
                                     number of files matching the query. When an 
                                     update causes the query results to change the
                                      number of matches is updated.  The find can 
                                     be cancelled by typing ctrl-C.
  
        --count
                                     Causes the mdfind command to output the total number of
                                     matches, instead of the path to the matching 
                                     items.
  
    -o, --onlyin dir                 mfd默认搜索文件系统中所有的被索引文件，通过本选项
                                     来约束其只在某个目录中进行搜索.
  
        --debug
                                     mfd 通过调用 OS X 系统自带的 mdfind 命令来完成文件搜索，指定
                                     本选项之后, 可以看到 mfd 实际调用的命令的参数
```

## 安装

```
git clone https://github.com/lululau/mfd
cd mfd
sudo cp mfd /usr/local/bin

mfd --help
```  