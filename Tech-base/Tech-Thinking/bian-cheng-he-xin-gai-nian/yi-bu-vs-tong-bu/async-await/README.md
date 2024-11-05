# async/await

`async` 和 `await` 是 Python 中用于实现异步编程的关键字，它们使得编写异步代码变得更加简洁和直观。它们是基于 **协程**（coroutines）实现的，协程本质上是能在某个点暂停执行并在以后恢复的函数。`async` 和 `await` 使得我们能够在非阻塞的情况下执行异步操作，如 I/O 操作、网络请求等。

#### 1. **`async` 关键字**

* `async` 用来定义一个**异步函数**（也叫协程函数）。异步函数的返回值是一个协程对象，通常需要用 `await` 来获取返回的结果。

**示例**：

```python
async def my_async_function():
    print("Start")
    await asyncio.sleep(1)  # 模拟异步操作（例如网络请求）
    print("End")
```

* 在这个例子中，`my_async_function` 是一个异步函数，它会先输出 `"Start"`，然后等待 1 秒后输出 `"End"`。`await` 会暂停协程的执行，直到 `asyncio.sleep(1)` 完成。

#### 2. **`await` 关键字**

* `await` 用来**暂停协程的执行**，等待一个异步操作完成，然后恢复执行。`await` 后面必须跟一个可等待对象（通常是一个异步函数或协程）。
* `await` 会将控制权交还给事件循环（Event Loop），让它去执行其他的任务。当 `await` 后的异步操作完成时，协程会恢复执行。

**示例**：

```python
async def main():
    print("Start")
    await my_async_function()  # 等待异步函数完成
    print("End")

asyncio.run(main())  # 运行主协程
```

这里，`main` 是一个异步函数，里面调用了另一个异步函数 `my_async_function`。`await` 会使 `main` 在 `my_async_function` 完成之前暂停执行，然后继续运行。

#### 3. **如何运行异步代码**

* 异步代码不能像普通的同步代码那样直接执行。它需要在**事件循环**（Event Loop）中运行，`asyncio.run()` 是最常见的启动事件循环的方法。

```python
import asyncio

async def my_async_function():
    await asyncio.sleep(1)
    print("Task completed!")

asyncio.run(my_async_function())  # 运行异步任务
```

`asyncio.run()` 会创建一个新的事件循环并执行指定的协程，直到任务完成。

#### 4. **`async` / `await` 与线程的关系**

* **异步（async/await）** 和 **多线程** 不同。`async` 和 `await` 并不会创建新的线程，而是通过在单线程中进行任务切换来实现并发执行。这种并发主要是由事件循环管理的，尤其适用于 I/O 密集型任务，而不适合计算密集型任务。
* 在单线程中，通过 `await` 可以让出控制权，允许其他协程在等待 I/O 操作（如网络请求、文件操作等）时继续执行其他任务。

#### 5. **使用 `async` 和 `await` 的优势**

* **非阻塞**：使用 `async` 和 `await`，可以在等待耗时的任务（如网络请求、数据库操作）时，不阻塞主线程。这样，程序可以在等待期间执行其他任务，提高效率。
* **简洁的代码**：与传统的回调或线程池方式相比，`async` / `await` 提供了一种更加清晰和易于理解的异步编程方式。
* **高效的并发**：`async` / `await` 使得应用可以处理大量并发任务，而不需要每个任务都创建一个新的线程，从而节省了系统资源。

#### 6. **`async` / `await` 与传统回调的对比**

| 特性       | `async`/`await`                  | 回调（Callback）         |
| -------- | -------------------------------- | -------------------- |
| **代码结构** | 代码看起来像同步代码，简洁明了                  | 回调函数导致代码层层嵌套（“回调地狱”） |
| **错误处理** | 使用 `try/except` 语句进行错误处理，像同步代码一样 | 错误处理通过传递错误到回调函数中实现   |
| **易读性**  | 更具可读性，流式代码执行，避免了嵌套回调             | 需要多层嵌套回调，导致代码难以理解    |
| **适用场景** | 非阻塞I/O操作，如文件读写、网络请求等             | 可以用于任何需要执行的回调任务      |

#### 7. **示例：异步编程的实际应用**

假设你想从多个网站异步下载网页内容，传统的同步编程方式会依次下载每个网页，导致浪费时间。使用 `async` 和 `await` 可以同时请求多个网页，而不会阻塞主程序。

```python
import asyncio
import aiohttp

async def fetch_url(url):
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

async def main():
    urls = ['https://www.example.com', 'https://www.python.org', 'https://www.google.com']
    tasks = [fetch_url(url) for url in urls]
    results = await asyncio.gather(*tasks)
    print(f"Fetched {len(results)} pages")

# 运行异步任务
asyncio.run(main())
```

在这个例子中，`fetch_url` 是一个异步函数，它用 `aiohttp` 发起异步网络请求。`asyncio.gather()` 会并发地执行多个异步任务，等待所有任务完成后，返回结果。

#### 总结

* **`async`** 用来定义异步函数，而 **`await`** 用来等待异步函数执行的结果。通过这两个关键字，Python 提供了一种简洁且强大的方式来编写并发程序，特别适合 I/O 密集型任务（如网络请求、文件操作等）。
* 异步编程允许你在等待某些操作完成时，继续执行其他操作，这提高了程序的效率和响应性，同时避免了阻塞现象。
