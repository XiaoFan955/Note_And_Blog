#### 字符串string相关函数

> 字符串读取 getline()

```c++
#include<string>
string s;
getline(s,cin);
```

> 获取子串 substr()

```c++
s.substr(起始位置，子串长度)
```

### sort函数的cmp函数

~~~c++
sort(v.begin(),v.end(),[&](int i,int j){return v[i]<v[j];})
~~~

延伸应用：利用iota函数生成一个索引列表，根据原数组对索引列表排序以达到不修改原数组就能获得排好序的索引的效果。

~~~c++
vector<int>index(n);
iota(index.begin(),index.end(),0);
sort(index.begin(),index.end(),[&](int i,int j){return heights[i]>heights[j];});
~~~

