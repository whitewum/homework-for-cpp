# p51 

## 2.23

不能 ，因为指针只相当于指向了一个地址，而地址中的内容是否有效是未知的`

2.24 因为lp指针的类型不是int，而用void\*定义了p相当于p是一个空指针，可以存放任何类型的对象

------

# p53

## 2.25  

### 1:

ip是一个int类指针型的，i是一个int型的变量，r是一个int型的引用。

### 2：

i是一个int型的变量，ip是一个空指针。

### 3：

ip是一个int类型的指针，ip2是一个int类型的变量。

------

# p62

## 2.35 

 i是一个int型常量，j是一个int型变量，p是一个指向int常量的指针，k是一个指向int常量的引用，j2是一个int型常量，k2是一个指向int常量的引用

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;typeinfo\&gt;

int main() {

  const int i = 42;

  auto j = i;

  const auto &amp;k = i;

  auto \*p = &amp;i;

  const auto j2 = i, &amp;k2 = i;

  std::cout \&lt;\&lt; &quot;i  is &quot; \&lt;\&lt; typeid(i).name() \&lt;\&lt; std::endl;

  std::cout \&lt;\&lt; &quot;j  is &quot; \&lt;\&lt; typeid(j).name() \&lt;\&lt; std::endl;

  std::cout \&lt;\&lt; &quot;k  is &quot; \&lt;\&lt; typeid(k).name() \&lt;\&lt; std::endl;

  std::cout \&lt;\&lt; &quot;p  is &quot; \&lt;\&lt; typeid(p).name() \&lt;\&lt; std::endl;

  std::cout \&lt;\&lt; &quot;j2 is &quot; \&lt;\&lt; typeid(j2).name() \&lt;\&lt; std::endl;

  std::cout \&lt;\&lt; &quot;k2 is &quot; \&lt;\&lt; typeid(k2).name() \&lt;\&lt; std::endl;

  std::cout \&lt;\&lt; std::boolalpha;

  std::cout \&lt;\&lt; &quot;i and j  have same type? &quot;

​```
        \&lt;\&lt; std::is\_same\&lt;decltype(i), decltype(j)\&gt;::value \&lt;\&lt; std::endl;
​```

  std::cout \&lt;\&lt; &quot;i and k  have same type? &quot;

​```
        \&lt;\&lt; std::is\_same\&lt;decltype(i), decltype(k)\&gt;::value \&lt;\&lt; std::endl;
​```

  std::cout \&lt;\&lt; &quot;i and j2 have same type? &quot;

​```
        \&lt;\&lt; std::is\_same\&lt;decltype(i), decltype(j2)\&gt;::value \&lt;\&lt; std::endl;
​```

  std::cout \&lt;\&lt; &quot;j and j2 have same type? &quot;

​```
        \&lt;\&lt; std::is\_same\&lt;decltype(j), decltype(j2)\&gt;::value \&lt;\&lt; std::endl;
​```

  std::cout \&lt;\&lt; &quot;k and k2 have same type? &quot;

​```
        \&lt;\&lt; std::is\_same\&lt;decltype(k), decltype(k2)\&gt;::value \&lt;\&lt; std::endl;
​```

  return 0;

}
```

------

# p81

## 3.4

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;string\&gt;

int main() {

​```
std::string str1, str2;

while (std::cin \&gt;\&gt; str1 \&gt;\&gt; str2) {

    if (str1 == str2)

        std::cout \&lt;\&lt; &quot;equal.&quot; \&lt;\&lt; std::endl;

    else

        std::cout \&lt;\&lt; ((str1 \&gt; str2) ? str1 : str2) \&lt;\&lt; std::endl;

}

return 0;
​```

}
```

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;string\&gt;

int main() {

​```
std::string str1, str2;

while (std::cin \&gt;\&gt; str1 \&gt;\&gt; str2) {

    if (str1.size() == str2.size())

        std::cout \&lt;\&lt; &quot;same&quot; \&lt;\&lt; std::endl;

    else

        std::cout \&lt;\&lt; ((str1.size() \&gt; str2.size()) ? str1 : str2) \&lt;\&lt; endl;

}

return 0;
​```

}
```



## 3.5

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;string\&gt;

int main() {

​```
std::string largeStr;

std::string str;

while (std::cin \&gt;\&gt; str) {

    largeStr += str;

}

std::cout \&lt;\&lt; largeStr \&lt;\&lt; std::endl;

return 0;
​```

}
```

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;string\&gt;

int main() {

​```
std::string largeStr;

std::string str;

while (std::cin \&gt;\&gt; str) {

    if (largeStr.empty())

        largeStr += str;

    else

        largeStr += &quot; &quot; + str;

}

std::cout \&lt;\&lt; largeStr \&lt;\&lt; std::endl;

return 0;
​```

}
```

------

# p94

## 3.20

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;vector\&gt;

using std::vector;

using std::cout;

using std::endl;

using std::cin;

int main() {

​```
vector\&lt;int\&gt; ivec;

int i;

while (cin \&gt;\&gt; i) ivec.push\_back(i);

if (ivec.empty()) {

    cout \&lt;\&lt; &quot;input at least one integer.&quot; \&lt;\&lt; endl;

    return -1;

} else if (ivec.size() == 1) {

    cout \&lt;\&lt; ivec[0] \&lt;\&lt; &quot; don&#39;t have any adjacent elements.&quot;;

} else {

    for (decltype(ivec.size()) i = 0; i != ivec.size() - 1; ++i)

        cout \&lt;\&lt; ivec[i] + ivec[i + 1] \&lt;\&lt; &quot; &quot;;

}

cout \&lt;\&lt; endl;

decltype(ivec.size()) size = ivec.size();

if (size % 2 != 0)

    size = size / 2 + 1;

else

    size /= 2;

for (decltype(ivec.size()) i = 0; i != size; ++i)

    cout \&lt;\&lt; ivec[i] + ivec[ivec.size() - i - 1] \&lt;\&lt; &quot; &quot;;

cout \&lt;\&lt; endl;

return 0;
​```

}
```

------

# p99

## 3.23

```
// copyright 2019 MoeKedama

#include \&lt;vector\&gt;

#include \&lt;iostream\&gt;

#include \&lt;iterator\&gt;

using std::vector;

using std::iterator;

using std::cout;

using std::endl;

int main() {

​```
vector\&lt;int\&gt; ivec(10, 1);

for (auto it = ivec.begin(); it != ivec.end(); ++it) \*it \*= 2;

for (auto value : ivec) cout \&lt;\&lt; value \&lt;\&lt; &quot; &quot;;

cout \&lt;\&lt; endl;

return 0;
​```

}
```

------

# p188

## 6.10

```
// copyright 2019 MoeKedama

#include \&lt;iostream\&gt;

#include \&lt;stdexcept\&gt;

#include \&lt;string\&gt;

using std::cin;

using std::cout;

using std::endl;

void swap(int\* const lhs, int\* const rhs) {

​```
auto tmp = \*lhs;

\*lhs = \*rhs;

\*rhs = tmp;
​```

}

int main() {

​```
for (int lht, rht; cin \&gt;\&gt; lht \&gt;\&gt; rht;) {

    swap(&amp;lht, &amp;rht);

    cout \&lt;\&lt; lht \&lt;\&lt; &quot; &quot; \&lt;\&lt; rht \&lt;\&lt; endl;

}
​```

}
```

------

# p193

## 6.19

### a：

非法，形参数只有一个

### b：

合法

### c：

合法

### d：

合法



------

# p210

## 6.39

### a：

非法

### b：

非法

### c：

合法



------

# p241

## 7.16

访问说明符出现的频率是没有限制的。指定的访问将保持有效，直到下一个访问说明符或类主体结束。程序所有部分都可以访问的成员应在公共说明符之后定义。访问说明符的作用域是说明下一个访问说明符或者类结束。不想被使用该类的程序看到的代码细节，都要private.

------

# p249

## 7.27

```
// copyright 2019 MoeKedama

#ifndef C7\_27\_h

#define C7\_27\_h

#include \&lt;string\&gt;

#include \&lt;iostream\&gt;

class Screen {

public:

​```
using pos = std::string::size\_type;

Screen() = default; // 1

Screen(pos ht, pos wd) : height(ht), width(wd), contents(ht \* wd, &#39; &#39;) {} // 2

Screen(pos ht, pos wd, char c) : height(ht), width(wd), contents(ht \* wd, c)

{

}

char get() const { return contents[cursor]; }

char get(pos r, pos c) const { return contents[r \* width + c]; }

inline Screen&amp; move(pos r, pos c);

inline Screen&amp; set(char c);

inline Screen&amp; set(pos r, pos c, char ch);

const Screen&amp; display(std::ostream&amp; os) const

{

    do\_display(os);

    return \*this;

}

Screen&amp; display(std::ostream&amp; os)

{

    do\_display(os);

    return \*this;

}
​```

private:

​```
void do\_display(std::ostream&amp; os) const { os \&lt;\&lt; contents; }
​```

private:

​```
pos cursor = 0;

pos height = 0, width = 0;

std::string contents;
​```

};

inline Screen&amp; Screen::move(pos r, pos c)

{

​```
cursor = r \* width + c;

return \*this;
​```

}

inline Screen&amp; Screen::set(char c)

{

​```
contents[cursor] = c;

return \*this;
​```

}

inline Screen&amp; Screen::set(pos r, pos c, char ch)

{

​```
contents[r \* width + c] = ch;

return \*this;
​```

}

#endif
```

------

# p266

## 7.49

### a：

合法

### b：

不合法，Salesdata&amp;类型与Salesdata类型之间不可转换

### c：

不合法，const不对，因为combine本身是需要改变传入参数的

------

# p272

## 7.58

rate在实际情况中是可变的。vec不需要在类内定义大小，可以在另一个.h文件中声明其大小。