# 交换两个数(不用临时变量)

{% hint style="info" %}
异或实现了交换
{% endhint %}



#### 不用临时变量怎么实现 swap(a, b)

```
void swap(int a, int b) {
    
    //int a =2, b=6;
    a = a ^ b;
    b = b ^ a;
    a = a ^ b;
    printf("a=%d, b=%d \n", a, b);
}

```
