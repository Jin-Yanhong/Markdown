## 字符串原生方法

| 方法名              | 语法                                          | 解释                                                                                           |
| ------------------- | --------------------------------------------- | :--------------------------------------------------------------------------------------------- |
| charAt()            | string.charAt(index)                          | 返回在指定位置的字符                                                                           |
| charCodeAt()        | string.charCodeAt(index)                      | 返回在指定的位置的字符的 Unicode 编码                                                          |
| concat()html)       | string.concat(string1, string2, ..., stringX) | 连接两个或更多字符串，并**返回新的字符串**                                                     |
| fromCharCode()      | string.fromCharCode(n1, n2, ..., nX)          | 将 Unicode 编码转为字符                                                                        |
| indexOf()           | string.indexOf(searchvalue,start)             | **返回某个指定的字符串值在字符串中首次出现的位置**                                             |
| includes()html)     | string.includes(searchvalue, start)           | **查找字符串中是否包含指定的子字符串**如果找到匹配的字符串返回 true，否则返回 false            |
| lastIndexOf()       | string.lastIndexOf(searchvalue,start)         | 从后向前搜索字符串，并从起始位置（0）开始计算返回字符串最后出现的位置                          |
| match()             | string.match(regexp)                          | 查找找到一个或多个正则表达式的匹配                                                             |
| repeat()            | string.repeat(count)                          | 复制字符串指定次数，并将它们连接在一起返回                                                     |
| replace()           | string.replace(searchvalue,newvalue)          | **在字符串中查找匹配的子串， 并替换与正则表达式匹配的子串**                                    |
| search()            | string.search(searchvalue)                    | **如果没有找到任何匹配的子串，则返回 -1 提取字符串的片断，并在新的字符串中返回被提取的部分**   |
| slice()html)        | string.slice(start,end)                       | **提取字符串的某个部分，并以新的字符串返回被提取的部分**                                       |
| split()             | string.split(separator,limit)                 | 把字符串分割为字符串数组，**不改变原始字符串**                                                 |
| startsWith()        | string.startsWith(searchvalue, start)         | 查看字符串是否以指定的子字符串开头**返回布尔值**                                               |
| substr()            | string.substr(start,length)                   | 从起始索引号提取字符串中指定数目的字符**不改变原来字符串**                                     |
| substring()         | string.substring(from, to)                    | 提取字符串中两个指定的索引号之间的字符**返回的子串包括 开始 处的字符，但不包括 结束 处的字符** |
| toLowerCase()       | string.toLowerCase()                          | 把字符串转换为小写                                                                             |
| toUpperCase()       | string.toUpperCase()                          | 把字符串转换为大写                                                                             |
| trim()              | string.trim()                                 | **去除字符串两边的空白**                                                                       |
| toLocaleLowerCase() | string.toLocaleLowerCase()                    | 根据本地主机的语言环境把字符串转换为小写                                                       |
| toLocaleUpperCase() | string.toLocaleUpperCase()                    | 根据本地主机的语言环境把字符串转换为大写                                                       |
| valueOf()html)      | string.valueOf()                              | 返回某个字符串对象的原始值通常由 JavaScript 在后台自动进行调用                                 |
| toString()          | string.toString()                             | 返回一个字符串                                                                                 |
