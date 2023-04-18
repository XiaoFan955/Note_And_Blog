# python数据处理与分析

#### pandas读取csv文件(读excel改为read_excel()函数即可)

```python
import pandas as pd
# 读取文件，DataFrame结构
df = pd.read_csv(file_path, encoding='utf_8_sig') 
```

#### pandas的处理dataframe数据

```python
# 取某一列，astype设置格式
col = df['列名'].astype(int)
# 将某列的值设置为行索引，注意访问的时候先列后行
df.set_index('列名', inplace=True)
# 删除行, 多行删除将行索引用列表表示
df.drop('行索引', axis=0, inplace=True)
```



## 绘图

#### 绘制散点图

```python
# 利用dataFrame直接画
import seaborn as sns
joint_clos = [
    'xxx',
    'xxx'
]
sns.pairplot(df[joint_clos], kind='scatter', diag_kind='kde')
```

