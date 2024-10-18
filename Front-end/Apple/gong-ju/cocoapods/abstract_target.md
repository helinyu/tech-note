# abstract\_target

在 CocoaPods 中，`abstract_target` 是用于在 Podfile 中定义一个抽象的 target，它本身不会生成具体的 Xcode target。相反，它允许你将多个 target 的通用依赖集中到一个地方进行管理，以减少重复配置。

#### 使用场景

当你的项目包含多个 target（例如多个 app 或多个 app 的不同版本），并且它们共享相同的依赖库时，可以使用 `abstract_target` 来避免在每个 target 中重复声明相同的依赖。它主要用于组织和结构化依赖的配置，而不会直接创建一个编译目标。

#### 示例

```ruby
abstract_target 'SharedPods' do
  pod 'Alamofire'
  pod 'SwiftyJSON'

  target 'AppA' do
    pod 'Firebase'
  end

  target 'AppB' do
    pod 'Realm'
  end
end
```

#### 解释：

1. `abstract_target 'SharedPods'` 是一个抽象的 target，用于共享公共的依赖。
2. `pod 'Alamofire'` 和 `pod 'SwiftyJSON'` 是两个公共依赖，会应用到 `AppA` 和 `AppB` 中。
3. `target 'AppA'` 和 `target 'AppB'` 是具体的应用 target，分别有自己特定的依赖（如 `Firebase` 和 `Realm`）。
4. 这样，`AppA` 和 `AppB` 都共享了 `Alamofire` 和 `SwiftyJSON`，但各自又有自己的独特依赖。

#### `abstract_target` 的特点：

* **不生成实际 target**：它不会在 Xcode 中生成具体的 target，而只是帮助你组织代码和依赖。
* **继承依赖**：其下的 target 会继承 `abstract_target` 中定义的所有依赖。

使用 `abstract_target` 可以让 Podfile 更加简洁易维护，尤其是在多 target 项目中有很多共享依赖时，它可以大大减少冗余。
