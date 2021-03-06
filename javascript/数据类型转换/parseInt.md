## parseInt

- parseInt(string,radix)：是用来解析字符串的，参数：

  - string：必选。要被解析的字符串。如果不是一个字符串，则将其转换为字符串，字符串的开关的空白符会被忽略
  - radix：可选，表示要解析的数字的基数，该值介于 2~36 之间；如果 radix 为 undefined 或者为 0 或者没有指定的情况下，会作如下处理：
    - 如果它以“0x”或“0X”开头，将以 16 为基数；
    - 如果字符串 string 以"0"开头，基数是 8（八进制）或者 10（十进制），具体是哪个基数由实现环境决定。ES5 规定使用 10，但是并不是所有浏览器都遵循这个规则，**因此，永远都要明确的给出 radix 参数的值**
    - 如果字符串 string 以其它任何值开头，则基数是 10（十进制）

  如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果该基数小于 2 或者大于 26，则 parseInt()将返回 NaN

- parseInt()方法用于将字符串作为有符号的十进制整数进行解析
- radix 指定的基数，将字符串参数解析为有符号的整数；比如参数"10"表示使用我们通常使用的十进制数值系统。
