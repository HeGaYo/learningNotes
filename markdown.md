this is an H1
=============
this is an H2
-------------
# this is 1
## this is 2
###### this is 5

> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
>
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.

--------
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
  consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
  Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
  Suspendisse id sem consectetuer libero luctus adipiscing.

--------
> This is the first level of quoting.
>
> This is nested blockquote.
>
> Back to the first level.
>
>     echo "hello world"

---------
> ## 这是一个标题。
>
> 1.   这是第一行列表项。
> 2.   这是第二行列表项。
>
> 给出一些例子代码：
>
>     return shell_exec("echo $input | $markdown_script");
>     echo "hello world"

--------
*   Red
*   Green
*   Blue


1.  Bird
2.  McHale
3.  Parish


-   Red
-   Green
-   Blue

--------
*   A list item with a blockquote:
*   加缩进
    > This is a blockquote
    > inside a list item.

-------
四个空格
这是一个普通段落：

    这是一个代码区块。

------
This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

-------
I get 10 times more traffic from [Google][] than from
[Yahoo][] or [MSN][].

  [google]: http://google.com/        "Google"
  [yahoo]:  http://search.yahoo.com/  "Yahoo Search"
  [msn]:    http://search.msn.com/    "MSN Search"

--------
*single asterisks*

_single underscores_

**double asterisks**

__double underscores__

--------
Use the `printf()` function.

-------
A single backtick in a code span: `` ` ``

A backtick-delimited string in a code span: `` `foo` ``

-------
`&#8212;` is the decimal-encoded equivalent of `&mdash;`.

Please don't use any `<blink>` tags.

-----
![Alt text](/path/to/img.jpg)

![Alt text](/path/to/img.jpg "Optional title")

-----
~~Mistaken text.~~

----
```
x = 0
x = 2 + 2
what is x
```

----
```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```

-----
```javascript
{"result":{"jane":0;"ann":1}}
```

-----
First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |

--------
