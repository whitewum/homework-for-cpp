# p51 

## 2.23

不能 ，因为指针只相当于指向了一个地址，而地址中的内容是否有效是未知的

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
#include <iostream>
#include <typeinfo>

int main() {
  const int i = 42;
  auto j = i;
  const auto &k = i;
  auto *p = &i;
  const auto j2 = i, &k2 = i;

  std::cout << "i  is " << typeid(i).name() << std::endl;
  std::cout << "j  is " << typeid(j).name() << std::endl;
  std::cout << "k  is " << typeid(k).name() << std::endl;
  std::cout << "p  is " << typeid(p).name() << std::endl;
  std::cout << "j2 is " << typeid(j2).name() << std::endl;
  std::cout << "k2 is " << typeid(k2).name() << std::endl;

  std::cout << std::boolalpha;

  std::cout << "i and j  have same type? "
            << std::is_same<decltype(i), decltype(j)>::value << std::endl;
  std::cout << "i and k  have same type? "
            << std::is_same<decltype(i), decltype(k)>::value << std::endl;
  std::cout << "i and j2 have same type? "
            << std::is_same<decltype(i), decltype(j2)>::value << std::endl;
  std::cout << "j and j2 have same type? "
            << std::is_same<decltype(j), decltype(j2)>::value << std::endl;
  std::cout << "k and k2 have same type? "
            << std::is_same<decltype(k), decltype(k2)>::value << std::endl;
  return 0;
}
```



------

# p81

## 3.4

```
// copyright 2019 MoeKedama
#include <iostream>
#include <string>

int main() {
    std::string str1, str2;
    while (std::cin >> str1 >> str2) {
        if (str1 == str2)
            std::cout << "equal." << std::endl;
        else

            std::cout << ((str1 > str2) ? str1 : str2) << std::endl;
    }

    return 0;
}

```

```
// copyright 2019 MoeKedama
#include <iostream>
#include <string>

int main() {
    std::string str1, str2;
    while (std::cin >> str1 >> str2) {
        if (str1.size() == str2.size())
            std::cout << "same" << std::endl;
        else
            std::cout << ((str1.size() > str2.size()) ? str1 : str2) << endl;
    }

    return 0;
}

```



## 3.5

```
// copyright 2019 MoeKedama
#include <iostream>
#include <string>

int main() {
    std::string largeStr;
    std::string str;
    while (std::cin >> str) {
        largeStr += str;
    }
    std::cout << largeStr << std::endl;

    return 0;
}

```

```
// copyright 2019 MoeKedama
#include <iostream>
#include <string>

int main() {
    std::string largeStr;
    std::string str;
    while (std::cin >> str) {
        if (largeStr.empty())
            largeStr += str;
        else
            largeStr += " " + str;
    }

    std::cout << largeStr << std::endl;
    return 0;
}

```

------

# p94

## 3.20

```
// copyright 2019 MoeKedama
#include <iostream>
#include <vector>

using std::vector;
using std::cout;
using std::endl;
using std::cin;

int main() {
    vector<int> ivec;
    int i;
    while (cin >> i) ivec.push_back(i);

    if (ivec.empty()) {
        cout << "input at least one integer." << endl;
        return -1;
    } else if (ivec.size() == 1) {
        cout << ivec[0] << " don't have any adjacent elements.";
    } else {
        for (decltype(ivec.size()) i = 0; i != ivec.size() - 1; ++i)
            cout << ivec[i] + ivec[i + 1] << " ";
    }
    cout << endl;

    decltype(ivec.size()) size = ivec.size();
    if (size % 2 != 0)
        size = size / 2 + 1;
    else
        size /= 2;

    for (decltype(ivec.size()) i = 0; i != size; ++i)
        cout << ivec[i] + ivec[ivec.size() - i - 1] << " ";
    cout << endl;

    return 0;
}

```

------

# p99

## 3.23

```
// copyright 2019 MoeKedama
#include <vector>
#include <iostream>
#include <iterator>

using std::vector;
using std::iterator;
using std::cout;
using std::endl;

int main() {
    vector<int> ivec(10, 1);
    for (auto it = ivec.begin(); it != ivec.end(); ++it) *it *= 2;
    for (auto value : ivec) cout << value << " ";
    cout << endl;

    return 0;
}

```

------

# p188

## 6.10

```
// copyright 2019 MoeKedama
#include <iostream>
#include <stdexcept>
#include <string>

using std::cin;
using std::cout;
using std::endl;

void swap(int* const lhs, int* const rhs) {
    auto tmp = *lhs;
    *lhs = *rhs;
    *rhs = tmp;
}

int main() {
    for (int lht, rht; cin >> lht >> rht;) {
        swap(&lht, &rht);
        cout << lht << " " << rht << endl;
    }
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
#ifndef C7_27_h
#define C7_27_h

#include <string>
#include <iostream>
class Screen {
public:
    using pos = std::string::size_type;
    Screen() = default; // 1
    Screen(pos ht, pos wd) : height(ht), width(wd), contents(ht * wd, ' ') {} // 2
    Screen(pos ht, pos wd, char c) : height(ht), width(wd), contents(ht * wd, c)
    {
    } 
    char get() const { return contents[cursor]; }
    char get(pos r, pos c) const { return contents[r * width + c]; }
    inline Screen& move(pos r, pos c);
    inline Screen& set(char c);
    inline Screen& set(pos r, pos c, char ch);

    const Screen& display(std::ostream& os) const
    {
        do_display(os);
        return *this;
    }
    Screen& display(std::ostream& os)
    {
        do_display(os);
        return *this;
    }

private:
    void do_display(std::ostream& os) const { os << contents; }

private:
    pos cursor = 0;
    pos height = 0, width = 0;
    std::string contents;
};

inline Screen& Screen::move(pos r, pos c)
{
    cursor = r * width + c;
    return *this;
}

inline Screen& Screen::set(char c)
{
    contents[cursor] = c;
    return *this;
}

inline Screen& Screen::set(pos r, pos c, char ch)
{
    contents[r * width + c] = ch;
    return *this;
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