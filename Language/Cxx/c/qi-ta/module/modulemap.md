# ModuleMap

下面是一个在 Objective-C 中使用 `modulemap` 生成模块的完整示例。假设你正在创建一个名为 `MyLibrary` 的模块，模块中包含几个头文件，目的是让其他项目可以轻松导入 `MyLibrary`。

#### 项目结构

假设 `MyLibrary` 的文件结构如下：

```
MyLibrary/
├── include/
│   ├── MyLibrary.h
│   ├── Foo.h
│   └── Bar.h
├── module.modulemap
└── src/
    ├── Foo.m
    └── Bar.m
```

* `include` 文件夹中包含了库的头文件。
* `src` 文件夹中包含了库的实现文件。
* `module.modulemap` 文件定义了模块内容。

#### 1. 创建头文件和实现文件

**`MyLibrary.h`**

这是模块的主头文件，用于包含其他头文件：

```objc
// MyLibrary.h
#import <Foundation/Foundation.h>
#import "Foo.h"
#import "Bar.h"

@interface MyLibrary : NSObject
- (void)printLibraryInfo;
@end
```

**`Foo.h` 和 `Foo.m`**

```objc
// Foo.h
#import <Foundation/Foundation.h>

@interface Foo : NSObject
- (void)fooMethod;
@end

// Foo.m
#import "Foo.h"

@implementation Foo
- (void)fooMethod {
    NSLog(@"Foo method called");
}
@end
```

**`Bar.h` 和 `Bar.m`**

```objc
// Bar.h
#import <Foundation/Foundation.h>

@interface Bar : NSObject
- (void)barMethod;
@end

// Bar.m
#import "Bar.h"

@implementation Bar
- (void)barMethod {
    NSLog(@"Bar method called");
}
@end
```

#### 2. 创建 Module Map 文件

在 `MyLibrary` 文件夹中创建 `module.modulemap` 文件，并添加以下内容：

```plaintext
// module.modulemap
module MyLibrary {
    umbrella header "MyLibrary.h" // 主头文件，包含 Foo 和 Bar
    export *                      // 导出所有内容
    module * {                    // 设为公开
        export *
    }
}
```

#### 3. 配置 Xcode

1. **Include Paths**: 在 Xcode 项目的构建设置中，确保包含路径（Header Search Paths）包含了 `MyLibrary/include` 目录。例如，设置为 `$(SRCROOT)/MyLibrary/include`。
2. **Enable Modules**: 确保 `Enable Modules (C and Objective-C)` 选项设为 `YES`。
3. **Module Map Path**: 设置 `Module Map File` 路径指向 `module.modulemap` 文件的目录，例如 `$(SRCROOT)/MyLibrary`。

#### 4. 使用模块

在其他项目中直接导入 `MyLibrary` 模块：

```objc
// Main.m
@import MyLibrary;

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Foo *foo = [[Foo alloc] init];
        [foo fooMethod];

        Bar *bar = [[Bar alloc] init];
        [bar barMethod];
    }
    return 0;
}
```

这样，`@import MyLibrary` 就会导入模块内的所有内容，无需逐个导入头文件。
