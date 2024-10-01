# 跑步同一个脚印问题

<pre class="language-txt" data-overflow="wrap"><code class="lang-txt">Martin’s father goes for a jog every morning. martin follows him several minutes later. his father starts at a position that is x1 meters away from their home and runs rectilinearly at a constant speed of v1 meters per step for n steps.
martin is standing at x2 meters away from his home. he wonders how fast he must run at some constant speed of v2 meters per step so as to maximize f, where f equals the number of his father's footsteps that martin will land on during his run. <a data-footnote-ref href="#user-content-fn-1">it is given that the first step that martin will land on, from his starting position, will have been landed on by his father.</a>
note that if more than one prospective velocity results in the same number of maximum common steps, output the highest prospective velocity as v2.
write an algorithm to help martin calculate f and v2.
input
the first line of the input consists of two space-separated integers - x1 and x2 representing the initial positions of martin’s father and martin, respectively.
the second line consists of two space-separated integers - v1 and n representing the velocity of the father and the number of steps taken by the father, respectively.
output
print two space-separated integers as maximum number of common footsteps f and respective speed v2. constraints
1 = x1 = 105
0 = x2 = x1
1 = v1 = 104
1 = n = 104
example
input:
3 2
2 20
output:
21 1
explanation:
martin can have a maximum of 21 common footsteps with a velocity of 1 m/step.

这里是问题的中文翻译：

---

马丁的父亲每天早上去慢跑。马丁在几分钟后跟着他的父亲出发。他的父亲从离家x1米的一个位置开始跑步，以每步v1米的速度直线奔跑，跑了n步。  
马丁站在离家x2米的位置。他想知道，他应该以每步v2米的速度跑步，以便尽可能多地踩在他父亲跑步的脚印上。已知马丁的第一个步伐将与他父亲的某一个步伐重合。

需要注意的是，如果多个潜在的速度v2可以使马丁踩在相同数量的父亲的脚印上，则输出最大的速度v2。

### 任务：
编写一个算法，帮助马丁计算他可以踩在多少个父亲的脚印上（f），以及对应的最优速度v2。

### 输入格式：
第一行输入包含两个用空格分隔的整数x1和x2，分别表示马丁的父亲和马丁的初始位置。  
第二行包含两个用空格分隔的整数v1和n，分别表示父亲的速度和父亲跑的步数。

### 输出格式：
输出两个用空格分隔的整数，表示最大数量的共同脚步数f以及对应的速度v2。

### 约束条件：
1 ≤ x1 ≤ 105  
0 ≤ x2 ≤ x1  
1 ≤ v1 ≤ 104  
1 ≤ n ≤ 104

### 输入示例：
</code></pre>

```txt
### 约束条件：
1 ≤ x1 ≤ 105  
0 ≤ x2 ≤ x1  
1 ≤ v1 ≤ 104  
1 ≤ n ≤ 104

### 输入示例：
3 2 
2 20

### 输出示例：
21 1
```



```

#include <iostream>
#include <vector>

using namespace std;

vector<int> commonFootSteps(int fatherPos, int martinPos, int velFather, int steps) {
    vector<int> answer(2, 0);
    vector<int> temp(steps + 1, 0);

    for (int i = 0; i <= steps; i++) {
        temp[i] = fatherPos + velFather * i - martinPos;
    }

    for (int i = 0; i <= steps; i++) {
        if (temp[i] < 0)
            continue;

        int v2 = temp[i];
        int count = 0;

        for (int j = i; j <= steps; j++) {
            if (temp[j] % v2 == 0)
                count++;
        }

        if (answer[0] <= count) {
            answer[0] = count;
            answer[1] = v2;
        }
    }

    return answer;
}

int main() {
    int x1, x2, v, n;
    cin >> x1 >> x2 >> v >> n;
    vector<int> result = commonFootSteps(x1, x2, v, n);

    for (int i : result)
        cout << i << " ";

    return 0;
}
```

[^1]: &#x20;重点
