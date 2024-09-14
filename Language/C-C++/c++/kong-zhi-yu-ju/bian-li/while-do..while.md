# while(do..while)

和C语言一样，没有啥区别



### next 迭代器和while的结合

```
#include <iostream>
#include <vector>

template<typename Iter>
Iter next(Iter it, int n = 1) {
    std::advance(it, n);
    return it;
}

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    auto it = vec.begin();

    while (it!= vec.end()) {
        std::cout << *it << " ";
        it = next(it);
    }

    return 0;
}
```
