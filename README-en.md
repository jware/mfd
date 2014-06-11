# Mfd

Spotlight is very easy to use OS X on a desktop search tool, mdfind is Spotlight's CLI frontend,
Although mdfind powerful enough, but the interface is very unfriendly, for example, to search for the computer 2013 file size is larger than 1MB
The jpg image files, you need a very complex commands. mfd on mdfind package, providing relatively easy to use interface


## Usage

```
mfd [options]

  To search for the file system to be Spotlight indexed files by specifying a number of options, and the logical relationship between each option by default
  Search for a file system all indexed documents, you can "-o" option to restrict its search only in one directory.  

  % mfd --content-type com.omnigroup.omnigraffle.graffle --from 2011/11/1 -t '2013-01-01 14:30:24'
  % mfd --query '关键字' --content-type 'com.adobe.pdf'
  % mfd -e mp3 -b10M

options:

  The following options are supported beginning with an "@" symbol, followed by a file name, which means that the value of this option from the given file extract:

    • -f, --from
    • -t, --to
    • -F, --from-create
    • -T, --to-create
    • -c, --content-type
    • -k, --kind
    • -b, --biggerthan
    • -s, --smallerthan

    -f, --from from                  e.g. --from 2010/1/1
                                     Search for "file was last modified time" equal to or later file at the specified time, the time format is "YYYY-mm-dd HH: MM: SS"
                                     Which can use any non-numeric character as a delimiter, you can specify only the date portion.
                                     In addition,-f option also supports specifying a number followed by a letter in the form specified time,
                                     Supported characters include: S, M, H, d, m, Y, respectively: seconds, minutes, hours,
                                     Days, months, years, of which equals 30 days a month, a year equals 365 days.
                                     For example, search last 10 days of the file:-f 10d 
  
    -t, --to to                      Search for "file was last modified time" equal to or earlier than the time specified file format with the "-f" option
  
    -F, --from-create from           search for "file creation time" equal to or later than the specified time file format with the "-f" option
  
    -T, --to-create to               Search for "file creation time" equal to or earlier than the time specified file format with the "-f" option
  
    -q, --query query                eg - query "keyword"
  
    -c, --content-type contenttype   e.g. --contenttype com.omnigroup.omnigraffle.graffle
                                     Search "kMDItemContentType" attribute value equal to the specified file, you can not
                                     Specify the complete Content Type, such as Content Type Ruby script
                                     As "public.ruby-script", but you can use the following command all all
                                     Ruby script file: mfd-c ruby
  
    -e, --type file-ext-name         e.g.  -e 'mp3'
                                     ContentType string inconvenient memories, in order to facilitate the use of this program will be used
                                     File type extension and associated ContentType string, you can use this option
                                     Specify the file extension you want to search, you can use the "-l" option to view all supported
                                     Prefix name and the associated
  
    -l, --list-types                 ContentType string inconvenient memories, in order to facilitate the use of this program will be used
                                     File type extension and associated ContentType string, use this option
                                     See all the extension and the associated support
  
    -k, --kind kind                  e.g. --kind "HTML Document"
                                     "-K" option is another option is used to specify the file type, which uses
                                     "KMDItemKind" attribute to search for a file, for example, search for messages:. "-K-mail messages."
                                     Safari search history: "-k 'Safari history items.'"
  
    -b, --bigger-than size           e.g. --bigger-than 100000
                                     Search for a file size greater than or equal to a given value of the file, you can use t, g, m, k and other units,
                                     E.g., greater than or equal to the search 1MB byte file: "-b 1m"
  
    -s, --smaller-than size          e.g. --smaller-than 100000
                                     Search for a file size less than or equal to a given value of the file, you can use t, g, m, k and other units,
                                     For example, the search is less than or equal to 1GB byte file: "-b 1G"
  
        --prop-eq arg_value
                                     e.g. --prop-eq FSSize@diary.txt
                                     Different types of files each have a variety of attributes, the attributes of the program supports more limited, if necessary
                                     According to other attributes comparison, use of this option and the following three with "--prop" 
                                     Heading options. OS X can be built by the "mdls" command to view a variety of file attributes,
                                     You can specify only "kMDItem" When the attribute name is generally "kMDItem" starts using these four options
                                     The latter part, the format for the value of the option "property @ filename", for example,
                                     Search a.txt file size is equal to all the files: --prop-eq FSSize @ / a.txt.
  
        --prop-ne arg_value
                                     e.g. --prop-ne FSSize@diary.txt
  
        --prop-le arg_value
                                     e.g. --prop-le FSSize@diary.txt
  
        --prop-ge arg_value
                                     e.g. --prop-ge FSSize@diary.txt
  
    -D, --downloadfrom url           search files downloaded from the URL
    -N, --name name                  search by file names, automatic support fuzzy matching, without specifying a wildcard
    -0, --Null                       Prints an ASCII NUL character after each result path. 
                                     This is useful when used in conjunction with 
                                     xargs -0.
        --live
                                     Causes the mdfind command to provide live-updates to the  
                                     number of files matching the query. When an 
                                     update causes the query results to change the
                                     number of matches is updated. The find can 
                                     be cancelled by typing ctrl-C.
  
        --count
                                     Causes the mdfind command to output the total number of
                                     matches, instead of the path to the matching 
                                     items.
  
    -o, --onlyin dir                 mfd default search the file system for all documents to be indexed by the option
                                     To restrict its search only in one directory.
  
        --debug
                                     mfd by calling the OS X system comes mdfind commands to complete the file search, specify
                                     After this option, you can see the actual call parameters mfd command
```

## Installation

```
git clone https://github.com/lululau/mfd
cd mfd
sudo cp mfd /usr/local/bin

mfd --help
```  
