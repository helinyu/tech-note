# 视图(View)

在 MySQL 中，**视图（View）是一种虚拟表，它是由一个查询结果集构成的数据库对象。视图并不实际存储数据，而是基于一个或多个基础表的查询定义**。

{% hint style="info" %}
大概就是自定义数据库中表的引用，按照我需要的内容，定义了对应的引用罢了。
{% endhint %}



**一、视图的特点**

1. 简化复杂查询
   * 可以将复杂的查询封装在视图中，使得后续对该数据的访问更加简单和直观。例如，如果有一个涉及多个表连接和复杂筛选条件的查询，可以创建一个视图来简化这个查询，以后只需要对视图进行查询即可。
   *   例如，假设有两个表`orders`和`customers`，要查询特定客户的订单信息，可以创建一个视图：

       ```sql
       CREATE VIEW customer_orders_view AS
       SELECT o.order_id, o.order_date, c.customer_name
       FROM orders o
       JOIN customers c ON o.customer_id = c.customer_id
       WHERE c.customer_name = '特定客户名称';
       ```
   * 之后就可以直接查询这个视图来获取特定客户的订单信息，而无需每次都重复编写复杂的连接和筛选条件。
2. 数据安全
   * 可以通过视图限制用户对基础表的访问权限。只授予用户对视图的访问权限，而不直接授予对基础表的权限，这样可以控制用户能够看到的数据范围。
   * 例如，可以创建一个视图只显示某些敏感数据的部分字段，或者只显示满足特定条件的数据，从而保护数据的安全性。
3. 逻辑数据独立性
   * 当基础表的结构发生变化时，如果视图的定义不依赖于变化的部分，那么可以在不影响使用视图的应用程序的情况下进行表结构的调整。
   * 例如，如果在基础表中添加了一个新的字段，但视图的查询不涉及这个字段，那么使用视图的应用程序无需进行任何修改。

**二、创建、修改和删除视图**

1. 创建视图
   *   使用`CREATE VIEW`语句来创建视图。语法如下：

       ```sql
       CREATE VIEW view_name AS
       SELECT column1, column2,...
       FROM table_name
       WHERE condition;
       ```
   *   例如：

       ```sql
       CREATE VIEW employee_info_view AS
       SELECT employee_id, first_name, last_name, department_name
       FROM employees
       JOIN departments ON employees.department_id = departments.department_id;
       ```
2. 修改视图
   * 使用`CREATE OR REPLACE VIEW`语句来修改视图。如果视图不存在，则创建一个新的视图；如果视图已存在，则替换现有的视图定义。
   *   例如：

       ```sql
       CREATE OR REPLACE VIEW employee_info_view AS
       SELECT employee_id, first_name, last_name, department_name, job_title
       FROM employees
       JOIN departments ON employees.department_id = departments.department_id
       JOIN jobs ON employees.job_id = jobs.job_id;
       ```
3. 删除视图
   *   使用`DROP VIEW`语句来删除视图。语法如下：

       ```sql
       DROP VIEW view_name;
       ```
   *   例如：

       ```sql
       DROP VIEW employee_info_view;
       ```

需要注意的是，视图的性能可能会受到基础表数据量和查询复杂性的影响。在使用视图时，应该考虑到性能优化，例如合理设计基础表的索引等。
