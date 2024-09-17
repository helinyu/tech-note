# 销售系统问题

<pre class="language-txt" data-overflow="wrap"><code class="lang-txt">
---

**Question**

A distributor distributes energy drinks in 34 oz cans to customers who each have a unique ID. It distributes the drinks according to the demand for them. It developed a system that handles all the transaction queries of the store. The system will handle two types of queries (i.e., query 1 and query 2). <a data-footnote-ref href="#user-content-fn-1">The first query determines if the customer's ID has already been logged, and, if so, it adds the quantity of the new sale to the previous quantity and updates the record. If the customer's ID has not been logged in before, then it will make a fresh entry. Query 2 retrieves the number of cans purchased by customers in the given range of customer ID. At the end of the day, the distributor must submit a report for all the type 2 queries.</a>

Write an algorithm to help the distributor find the answer for all the type 2 queries.

**Input**
- The first line of the input consists of an integer `numOfCustomer`, representing the number of customers (C).
- The second line consists of two space-separated integers - `numOfQueries` and `queryDesc` representing the number of queries (Q) and the description of queries (queryDesc = 3 always), respectively.
- The next Q lines consist of three space-separated integers, wherein the first integer represents the type of the query and can only be 1 or 2. If the first integer is 1, then it is a type 1 query and the second and third integers represent the customer ID and the quantity of drinks purchased, respectively. If the first integer is 2, then it is a type 2 query, and the second and third integers represent the starting and ending customer ID range (both inclusive).

**Output**
Print space-separated integers representing the answer to all the type 2 queries. If no type 2 query is present, then do not print anything in the output.

**Constraints**
- \( 0 \leq numOfCustomer \leq 10^5 \)
- \( 0 \leq numOfQueries \leq 10^5 \)
- queryDesc = 3

**Example**
</code></pre>

Input: 4 5 3 1 3 12 2 0 2 1 1 4 1 3 2 2 2 4

```

---


#include <iostream>
#include <map>
#include <vector>
using namespace std;

// 处理查询的函数
vector<int> process_queries(int numOfCustomer,  vector<vector<int>>& queries) {
    map<int, int> customer_data;  // 存储客户ID和购买数量
    vector<int> results;  // 存储类型2查询的结果

    // 使用传统的for循环，基于索引访问queries
    int numOfQueries = queries.size();
    for (int i = 0; i < numOfQueries; ++i) {
        int query_type = queries[i][0];

        if (query_type == 1) {
            // 处理类型1查询 (记录销售)
            int customer_id = queries[i][1];
            int quantity = queries[i][2];

            // 如果客户已存在，则累加，否则创建新记录
            if (customer_data.find(customer_id) != customer_data.end()) {
                customer_data[customer_id] += quantity;
            } else {
                customer_data[customer_id] = quantity;
            }
        } else if (query_type == 2) {
            // 处理类型2查询 (范围查询)
            int start_id = queries[i][1];
            int end_id = queries[i][2];
            int total_quantity = 0;

            // 累加在给定范围内客户的购买数量
            for (int cid = start_id; cid <= end_id; ++cid) {
                if (customer_data.find(cid) != customer_data.end()) {
                    total_quantity += customer_data[cid];
                }
            }
            results.push_back(total_quantity);  // 将结果加入结果集
        }
    }

    return results;
}

int main() {
    // 示例输入
    int numOfCustomer = 4;

    vector<vector<int>> queries = {
        {1, 3, 12},
        {2, 0, 2},
        {1, 1, 4},
        {1, 3, 2},
        {2, 1, 4}
    };

    // 调用函数处理查询
    vector<int> results = process_queries(numOfCustomer, queries);

    // 使用传统的for循环输出结果
    for (int i = 0; i < results.size(); ++i) {
        cout << results[i] << " ";
    }
    cout << endl;

    return 0;
}


```

[^1]: 1/记录数据 2/是范围内查询数据
