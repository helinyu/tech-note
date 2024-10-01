# 模板特化

这段代码定义了一个名为`DenseMapInfo`的模板结构体，主要用于为不同类型的键提供一些操作，如空键、墓碑键（表示已删除的键）、哈希值计算和相等性比较。这种结构在哈希表或映射（如LLVM的`DenseMap`）中常用，用于管理键的状态和处理散列操作。

我们将分部分解释各个重要组件：

#### 1. **`DenseMapInfo`模板结构体**

* **作用**：`DenseMapInfo`为每种类型提供一个接口，支持几个通用操作：
  * `getEmptyKey()`: 返回一个特定的“空键”，即一个在散列表中不会自然出现的特殊值，表示没有数据。
  * `getTombstoneKey()`: 返回一个“墓碑键”，表示该键曾存在但被删除。
  * `getHashValue()`: 计算给定键的哈希值。
  * `isEqual()`: 判断两个键是否相等。
* **泛型化**：不同类型的键需要特定的处理方式，因此使用了模板特化的方式对不同类型（如指针类型、字符串、整数、浮点数等）分别定义了相应的处理逻辑。

#### 2. **为指针类型的特化**

```cpp
template<typename T>
struct DenseMapInfo<T*> {
  static inline T* getEmptyKey() {
    uintptr_t Val = static_cast<uintptr_t>(-1);
    return reinterpret_cast<T*>(Val);
  }
  static inline T* getTombstoneKey() {
    uintptr_t Val = static_cast<uintptr_t>(-2);
    return reinterpret_cast<T*>(Val);
  }
  static unsigned getHashValue(const T *PtrVal) {
      return ptr_hash((uintptr_t)PtrVal);
  }
  static bool isEqual(const T *LHS, const T *RHS) { return LHS == RHS; }
};
```

* 对于指针类型，空键为`(T*)(-1)`，墓碑键为`(T*)(-2)`，哈希值是通过`ptr_hash`函数计算的。
* `isEqual`函数直接比较两个指针是否相等。

#### 3. **为`DisguisedPtr`类型的特化**

```cpp
template<typename T>
struct DenseMapInfo<DisguisedPtr<T>> {
  static inline DisguisedPtr<T> getEmptyKey() {
    return DisguisedPtr<T>((T*)(uintptr_t)-1);
  }
  static inline DisguisedPtr<T> getTombstoneKey() {
    return DisguisedPtr<T>((T*)(uintptr_t)-2);
  }
  static unsigned getHashValue(const T *PtrVal) {
      return ptr_hash((uintptr_t)PtrVal);
  }
  static bool isEqual(const DisguisedPtr<T> &LHS, const DisguisedPtr<T> &RHS) {
      return LHS == RHS; 
  }
};
```

* `DisguisedPtr`是用于隐匿指针的特殊类型，这里的特化同样提供了类似指针类型的空键、墓碑键以及哈希和比较逻辑。

#### 4. **为字符串的特化**

```cpp
template<>
struct DenseMapInfo<const char*> {
  static inline const char* getEmptyKey() { 
    return reinterpret_cast<const char *>((intptr_t)-1); 
  }
  static inline const char* getTombstoneKey() { 
    return reinterpret_cast<const char *>((intptr_t)-2); 
  }
  static unsigned getHashValue(const char* const &Val) { 
    return _objc_strhash(Val); 
  }
  static bool isEqual(const char* const &LHS, const char* const &RHS) {
    if (LHS == RHS) {
      return true;
    }
    if (LHS == getEmptyKey() || RHS == getEmptyKey()) {
      return false;
    }
    if (LHS == getTombstoneKey() || RHS == getTombstoneKey()) {
      return false;
    }
    return 0 == strcmp(LHS, RHS);
  }
};
```

* **空键和墓碑键**：特化为字符串的空键和墓碑键分别是`(char*)(-1)`和`(char*)(-2)`。
* **哈希函数**：使用了一个名为`_objc_strhash`的哈希函数，计算字符串的哈希值。
* **相等判断**：首先通过指针比较字符串是否相同，如果不同且不是空键或墓碑键，使用`strcmp`函数进行比较。

#### 5. **为基本类型的特化（如`char`、`int`、`unsigned`等）**

例如：

```cpp
template<>
struct DenseMapInfo<char> {
  static inline char getEmptyKey() { return ~0; }
  static inline char getTombstoneKey() { return ~0 - 1; }
  static unsigned getHashValue(const char& Val) { return Val * 37U; }
  static bool isEqual(const char &LHS, const char &RHS) {
    return LHS == RHS;
  }
};
```

* 基本类型（如`char`、`int`、`unsigned`）的特化为每种类型提供了合适的空键和墓碑键。
* 哈希值通过乘以某个固定的质数（如`37U`）来计算。
* 比较函数直接通过`==`操作符比较。

#### 6. **为`std::pair`类型的特化**

```cpp
template<typename T, typename U>
struct DenseMapInfo<std::pair<T, U> > {
  typedef std::pair<T, U> Pair;
  typedef DenseMapInfo<T> FirstInfo;
  typedef DenseMapInfo<U> SecondInfo;

  static inline Pair getEmptyKey() {
    return std::make_pair(FirstInfo::getEmptyKey(),
                          SecondInfo::getEmptyKey());
  }
  static inline Pair getTombstoneKey() {
    return std::make_pair(FirstInfo::getTombstoneKey(),
                          SecondInfo::getTombstoneKey());
  }
  static unsigned getHashValue(const Pair& PairVal) {
    uint64_t key = (uint64_t)FirstInfo::getHashValue(PairVal.first) << 32
          | (uint64_t)SecondInfo::getHashValue(PairVal.second);
    // 混合哈希函数
    key += ~(key << 32);
    key ^= (key >> 22);
    key += ~(key << 13);
    key ^= (key >> 8);
    key += (key << 3);
    key ^= (key >> 15);
    key += ~(key << 27);
    key ^= (key >> 31);
    return (unsigned)key;
  }
  static bool isEqual(const Pair &LHS, const Pair &RHS) {
    return FirstInfo::isEqual(LHS.first, RHS.first) &&
           SecondInfo::isEqual(LHS.second, RHS.second);
  }
};
```

* 对于`std::pair`类型，分别对`first`和`second`调用各自的`DenseMapInfo`。
* 哈希值由两个键的哈希值组合而成，使用了一种混合哈希算法。
* 比较函数则依次比较`first`和`second`的值。

#### 7. **`DenseMapValueInfo`**

```cpp
template<typename T>
struct DenseMapValueInfo {
    static inline bool isPurgeable(const T &value) {
        return false;
    }
};
```

* 这是一个辅助结构体，用于提供`isPurgeable`函数判断某个值是否可以被清除。默认实现返回`false`，表示不可清除。

#### 总结

这段代码定义了一组模板结构体`DenseMapInfo`，用于支持不同类型键的哈希表操作。它为多种类型（指针、字符串、整数、`std::pair`等）提供了如何生成哈希值、如何判断键相等、如何处理空键和墓碑键的特化。
