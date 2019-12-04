## P301 9.11

```
vector<int> vec;    // 0
vector<int> vec(10);    // 0
vector<int> vec(10,1);  // 1
vector<int> vec{1,2,3,4,5}; // 1,2,3,4,5
vector<int> vec(other_vec); // 和other_vec一样的vector
vector<int> vec(other_vec.begin(), other_vec.end()); //和other_vec一样的vector
```

------



## P309 9.20

```
#include <iostream>
#include <deque>
#include <list>
using std::deque;
using std::list;
using std::cout;
using std::cin;
using std::endl;

int main()
{
    list<int> l{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    deque<int> odd, even;
    for (auto i : l) (i & 0x1 ? odd : even).push_back(i);

    for (auto i : odd) cout << i << " ";
    cout << endl;
    for (auto i : even) cout << i << " ";
    cout << endl;

    return 0;
}
```

------



## P315 9.29

```
vec.resize(100);    //把vec加到100个元素
vec.resize(10);     //把后面90个元素擦除
```

------



## P324 9.43

```
#include <iostream>
#include <string>
using std::string;

void Replace(string& s, const string& oldVal, const string& newVal)
{
    for (auto beg = s.begin(); std::distance(beg, s.end()) >=
                               std::distance(oldVal.begin(), oldVal.end());) {
        if (string{beg, beg + oldVal.size()} == oldVal) {
            beg = s.erase(beg, beg + oldVal.size());
            beg = s.insert(beg, newVal.cbegin(), newVal.cend());
            std::advance(beg, newVal.size());
        }
        else
            ++beg;
    }
}

int main()
{
    {
        string str{"abcdedfefdaadf thru, tho gedryhgdfghaftghds."};
        Replace(str, "thru", "through");
        Replace(str, "tho", "though");
        std::cout << str << std::endl;
    }
    return 0;
}
```

------



## P331 9.52

```
#include <stack>
#include <string>
#include <iostream>

using std::stack;
using std::string;
using std::cout;
using std::endl;

int main()
{
string output;
    auto& expr = "ab (cd(ef)((((ggggggg))))) h (zxc) wert";
    auto repl = '#';
    auto seen = 0;
    stack<char> stk;

    for (auto c : expr) {
        stk.push(c);
        if (c == '(') ++seen;   
        if (seen && c == ')') { 
            while (stk.top() != '(') stk.pop();
            stk.pop();     
            stk.push(repl); 
            --seen; 
        }
    }
    for (; !stk.empty(); stk.pop()) output.insert(output.begin(), stk.top());
    cout << output << endl; 
}
```

------



## P339 10.3

```
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <numeric>

int main()
{
    std::vector<int> v = {1, 2, 3, 4};
    std::cout << std::accumulate(v.cbegin(), v.cend(), 0)
              << std::endl;
    return 0;
}
```

------



## P349 10.15

```
int i = 42;
auto add = [i](int num){return i + num;};
```

------



## P365 10.34

```
#include <iostream>
#include <algorithm>
#include <list>
#include <vector>

int main()
{
    std::vector<int> v = {4, 5, 7, 9, 6, 3, 1, 0, 2, 3};

    for (auto iter = v.crbegin(); iter != v.crend(); ++iter)
        std::cout << *iter << " ";
    std::cout << std::endl;
}
```

------



## P370 10.42

```
#include <iostream>
#include <string>
#include <list>

using std::string;
using std::list;

void elimDups(list<string>& words)
{
    words.sort();
    words.unique();
}

int main()
{
    list<string> l = {"aa", "aa", "aa", "aa", "aasss", "aa"};
    elimDups(l);
    for (const auto& e : l) std::cout << e << " ";
    std::cout << std::endl;
}
```

------



## P381 11.12

```
#include <vector>
#include <utility>
#include <string>
#include <iostream>

int main()
{
    std::vector<std::pair<std::string, int>> vec;
    std::string str;
    int i;
    while (std::cin >> str >> i)
        vec.push_back(std::pair<std::string, int>(str, i));

    for (const auto& p : vec)
        std::cout << p.first << ":" << p.second << std::endl;
}
```

------



## P383 11.17

```
#include <iostream>
#include <map>
#include <string>
#include <algorithm>

int main()
{
    std::map<std::string, std::vector<std::string>> famls;

    std::string lastName, chldName;

    while ([&]() -> bool {
        std::cout << "enter last name:\n";

        return std::cin >> lastName && lastName != "@q";
    }())

    {
        std::cout << "Enter children's name:\n";
        while (std::cin >> chldName && chldName != "@q") {
            famls[lastName].push_back(chldName);
        }
    }

    for (auto e : famls) {
        std::cout << e.first << ":\n";

        for (auto c : e.second) std::cout << c << " ";
        std::cout << "\n";
    }

    return 0;
}
```



## P396 11.38

```
#include <unordered_map>
#include <set>
#include <string>
#include <iostream>
#include <fstream>
#include <sstream>

using std::string;

void wordCounting()
{
    std::unordered_map<string, size_t> word_count;
    for (string word; std::cin >> word; ++word_count[word])
        ;
    for (const auto& w : word_count)
        std::cout << w.first << " occurs " << w.second
                  << (w.second > 1 ? "times" : "time") << std::endl;
}

void wordTransformation()
{
    std::ifstream ifs_map("../data/word_transformation.txt"),
        ifs_content("../data/given_to_transform.txt");
    if (!ifs_map || !ifs_content) {
        std::cerr << "can't find the documents." << std::endl;
        return;
    }

    std::unordered_map<string, string> trans_map;
    for (string key, value; ifs_map >> key && getline(ifs_map, value);)
        if (value.size() > 1)
            trans_map[key] =
                value.substr(1).substr(0, value.find_last_not_of(' '));

    for (string text, word; getline(ifs_content, text); std::cout << std::endl)
        for (std::istringstream iss(text); iss >> word;) {
            auto map_it = trans_map.find(word);
            std::cout << (map_it == trans_map.cend() ? word : map_it->second)
                      << " ";
        }
}

int main()
{
    wordTransformation();
}
```

------



## P446 13.12

```
3次，accum, item1和item2.
```

------



## P452 13.18

```
int Employee::s_increment = 0;

Employee::Employee()
{
    id_ = s_increment++;
}

Employee::Employee(const string& name)
{
    id_ = s_increment++;
    name_ = name;
}
```

------



## P472 13.46

```
int f();
vector<int> vi(100);
int&& r1 = f();
int& r2 = vi[0];
int& r3 = r1;
int&& r4 = vi[0] * f();
```

------



## P481 13.49

```
String& String::operator=(String&& rhs) NOEXCEPT
{
	if (this != &rhs) {
		free();
		elements = rhs.elements;
		end = rhs.end;
		rhs.elements = rhs.end = nullptr;
	}
	return *this;
}
String::String(String&& s) NOEXCEPT : elements(s.elements), end(s.end)
{
	s.elements = s.end = nullptr;
}

```

------



## P485 13.58

```
#include <vector>
#include <iostream>
#include <algorithm>

using std::vector;
using std::sort;

class Foo {
public:
    Foo sorted()&&;
    Foo sorted() const&;

private:
    vector<int> data;
};

Foo Foo::sorted() &&
{
    sort(data.begin(), data.end());
    std::cout << "&&" << std::endl; 
    return *this;
}

Foo Foo::sorted() const &
{

    std::cout << "const &" << std::endl; 


    return Foo(*this).sorted(); 
}

int main()
{
    Foo().sorted(); 
    Foo f;
    f.sorted(); 
}
```

------



## P493 14.3

```
(a)都不是 (b) string (c) vector (d) string
```

------



## P500 14.20

```
Sales_data::Sales_data(std::istream& is) : Sales_data()
{
    is >> *this;
}

Sales_data& Sales_data::operator+=(const Sales_data& rhs)
{
    units_sold += rhs.units_sold;
    revenue += rhs.revenue;
    return *this;
}

std::istream& operator>>(std::istream& is, Sales_data& item)
{
    double price = 0.0;
    is >> item.bookNo >> item.units_sold >> price;
    if (is)
        item.revenue = price * item.units_sold;
    else
        item = Sales_data();
    return is;
}

std::ostream& operator<<(std::ostream& os, const Sales_data& item)
{
    os << item.isbn() << " " << item.units_sold << " " << item.revenue << " "
       << item.avg_price();
    return os;
}

Sales_data operator+(const Sales_data& lhs, const Sales_data& rhs)
{
    Sales_data sum = lhs;
    sum += rhs;
    return sum;
}
```

------



## P509 14.38

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <string>
#include <fstream>

class BoundTest {
public:
    BoundTest(std::size_t l = 0, std::size_t u = 0) : lower(l), upper(u) {}
    bool operator()(const std::string& s)
    {
        return lower <= s.length() && s.length() <= upper;
    }

private:
    std::size_t lower;
    std::size_t upper;
};

int main()
{
    std::ifstream fin("../data/storyDataFile.txt");

    std::size_t quantity9 = 0, quantity10 = 0;
    BoundTest test9(1, 9);
    BoundTest test10(1, 10);

    for (std::string word; fin >> word;) {
        if (test9(word)) ++quantity9;
        if (test10(word)) ++quantity10;
    }

    std::cout << quantity9 << ", " << quantity10 << std::endl;
}
```

------



## P522 14.52

```
struct LongDouble {
};
LongDouble operator+(LongDouble&, double); 
SmallInt si;
LongDouble ld;
ld = si + ld;
ld = ld + si;
```

------



## P539 15.12

```
有
override：使得我们的意图更加清晰明确地告诉编译器我们想要覆盖掉已存在的虚函数。
final：如果我们将某个函数定义成final，则不允许后续的派生类来覆盖这个函数，否则会报错。

```

------



## P542 15.16

```
#ifndef CP5_EX15_16_LIMIT_QUOTE_H_
#define CP5_EX15_16_LIMIT_QUOTE_H_

#include "ex15_15_Disc_quote.h"
#include <string>

namespace EX16 {
    using std::string;
    using std::cout; using std::endl;
    using namespace EX15;

class Limit_quote : public Disc_quote {
public:
    Limit_quote() = default;
    Limit_quote(string const& book, double p, size_t min, size_t max, double dist) : Disc_quote(book, p, min, dist), max_qty(max) {}

    double net_price(size_t cnt) const final override {
        if (cnt > max_qty) return max_qty * (1 - discount) * price + (cnt - max_qty) * price;
        else if (cnt >= quantity) return cnt * (1 - discount) * price;
        else return cnt * price;
    }

private:
    size_t max_qty = 0;
};
}

#endif 
```

------



## P562 15.30

```
#ifndef CP5_EX15_30_BASKET_H
#define CP5_EX15_30_BASKET_H

#include <memory>
#include <set>
#include "ex15_30_Quote_Bulk_quote.h"

namespace EX30 {
    using std::shared_ptr;

    class Basket {
    public:
        Basket() = default;
        void add_item(const Quote &sale) { items.insert(shared_ptr<Quote>(sale.clone())); }
        void add_item(Quote &&sale) { items.insert(shared_ptr<Quote>(std::move(sale).clone())); }
        inline double total_receipt(std::ostream&) const;
    private:
        static bool compare(const shared_ptr<Quote> &lhs, const shared_ptr<Quote> &rhs) {
            return lhs->isbn() < rhs->isbn();
        }
        std::multiset<shared_ptr<Quote>, decltype(compare)*> items{compare};
    };

    inline double Basket::total_receipt(std::ostream &os) const {
        auto sum = 0.0;
        for (auto iter = items.cbegin(); iter != items.cend(); iter = items.upper_bound(*iter)) {
            sum += print_total(os, **iter, items.count(*iter));
        }
        os << "Total Sale: " << sum << std::endl;
        return sum;
    }
}

#endif 
```

------

