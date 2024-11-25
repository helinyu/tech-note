# 数组操作bug

2017-06-22 16:45:42.229 ViewTest\[2638:c07] \*\*\* Terminating app due to uncaught exception 'NSGenericException', reason: '\*\*\* Collection <\_\_NSArrayM: 0xb550c30> was mutated while being enumerated.'

当程序出现这个提示的时候，是因为你一边便利数组，又同时修改这个数组里面的内容，导致崩溃，网上的方法如下：

&#x20;

&#x20;NSMutableArray \* arrayTemp = xxx;&#x20;

&#x20;   NSArray \* array = \[NSArray arrayWithArray: arrayTemp]; &#x20;

&#x20;   for (NSDictionary \* dic in array) {       &#x20;

&#x20;       if (condition){           &#x20;

&#x20;           \[arrayTemp removeObject:dic];

&#x20;       }      &#x20;

&#x20;   }
