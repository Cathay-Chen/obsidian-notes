
`strings` 包是 Go 标准库中处理字符串的包，提供了许多关于字符串的方法。下面是该包中一些常用的方法：

1.  `func Compare(a, b string) int`

比较两个字符串大小，如果 a < b 则返回 -1，如果 a == b 则返回 0，如果 a > b 则返回 1。

2.  `func Contains(s, substr string) bool`

判断字符串 s 是否包含子串 substr，包含则返回 true，否则返回 false。

3.  `func Count(s, substr string) int`

统计字符串 s 中含有多少个子串 substr。

4.  `func Fields(s string) []string`

将字符串 s 按照空格符分割成多个子串，返回一个切片。

5.  `func HasPrefix(s, prefix string) bool`

判断字符串 s 是否以 prefix 开头，是则返回 true，否则返回 false。

6.  `func HasSuffix(s, suffix string) bool`

判断字符串 s 是否以 suffix 结尾，是则返回 true，否则返回 false。

7.  `func Index(s, substr string) int`

返回字符串 s 中子串 substr 在 s 中第一次出现的位置，如果不存在则返回 -1。

8.  `func Join(elems []string, sep string) string`

将一个字符串切片 elems 中的所有元素按照分隔符 sep 进行连接，返回连接后的字符串。

9.  `func Repeat(s string, count int) string`

将字符串 s 重复 count 次后返回。

10.  `func Replace(s, old, new string, n int) string`

将字符串 s 中前 n 个 old 替换为 new，返回替换后的字符串。

11.  `func Split(s, sep string) []string`

将字符串 s 按照分隔符 sep 分割成多个子串，返回一个切片。

12.  `func ToLower(s string) string`

将字符串 s 中的所有字符转换成小写后返回。

13.  `func ToUpper(s string) string`

将字符串 s 中的所有字符转换成大写后返回。

14.  `func Trim(s string, cutset string) string`

将字符串 s 中的前后端 cutset 中包含的字符全部去掉后返回。如果 cutset 为空，则默认将空格符去掉。

15.  `func TrimLeft(s string, cutset string) string`

将字符串 s 中的前端 cutset 中包含的字符全部去掉后返回。如果 cutset 为空，则默认将空格符去掉。

16.  `func TrimRight(s string, cutset string) string`

将字符串 s 中的后端 cutset 中包含的字符全部去掉后返回。如果 cutset 为空，则默认将空格符去掉。

这些方法是 Go 中常用的字符串处理函数。有了这些函数，我们可以方便地进行字符串的操作，提高开发效率和代码可读性。