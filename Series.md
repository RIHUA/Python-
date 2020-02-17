```python
import pandas as pd
```


```python
from pandas import Series, DataFrame
```


```python
import numpy as np
```


```python
#Series由⼀组数据（各种NumPy数据类型）以及⼀组与之相关的数据标签（即索引）组成。
obj = pd.Series([4,7,-5,3])
obj
```




    0    4
    1    7
    2   -5
    3    3
    dtype: int64




```python
obj2 = pd.Series([4,7,-5,3],index = ['d','b','a','c',])
obj2
```




    d    4
    b    7
    a   -5
    c    3
    dtype: int64




```python
obj2['a']
```




    -5




```python
obj2[['c', 'a', 'd']]#注意索引多个值需要以列表格式[]索引
```




    c    3
    a   -5
    d    4
    dtype: int64




```python
obj2[obj2>0]#使⽤NumPy函数或类似NumPy的运算都会保留索引值的链接
```




    d    4
    b    7
    c    3
    dtype: int64




```python
obj2 * 2
```




    d     8
    b    14
    a   -10
    c     6
    dtype: int64




```python
np.exp(obj2)
```




    d      54.598150
    b    1096.633158
    a       0.006738
    c      20.085537
    dtype: float64




```python
#还可以将Series看成是⼀个定⻓的有序字典，因为它是索引值到数据值的⼀个映射：
'b' in obj2
```




    True




```python
#如果数据被存放在⼀个Python字典中，也可以直接通过这个字典来创建Series
#Series的索引是原字典的索引
dic = {'Ohio':35000,'Texas':71000,'Oregon':16000,'Utah':5000,}
obj3 = pd.Series(dic)
obj3
```




    Ohio      35000
    Texas     71000
    Oregon    16000
    Utah       5000
    dtype: int64




```python
#通过传入一个排序好的索引以改变Series的索引的顺序
#如果states中存在原Series没有的索引，则新Series中该索引的结果对应NaN，用于表示缺失或NA值
#如果原Series的索引不存在于states中，则不会在新的Series中显示
states = ['California', 'Ohio', 'Oregon','Texas']              
obj4 = pd.Series(dic,index = states)
obj4
```




    California        NaN
    Ohio          35000.0
    Oregon        16000.0
    Texas         71000.0
    dtype: float64




```python
#Pandas中的isnull和notnull函数可用于检测缺失数据
pd.isnull(obj4)
```




    California     True
    Ohio          False
    Oregon        False
    Texas         False
    dtype: bool




```python
obj4.notnull()
```




    California    False
    Ohio           True
    Oregon         True
    Texas          True
    dtype: bool




```python
#对于许多应⽤⽽⾔，Series最重要的⼀个功能是，它会根据运算的索引标签⾃动对⻬数据
obj4
```




    California        NaN
    Ohio          35000.0
    Oregon        16000.0
    Texas         71000.0
    dtype: float64




```python
obj3
```




    Ohio      35000
    Texas     71000
    Oregon    16000
    Utah       5000
    dtype: int64




```python
obj3+obj4
#结果是两者相加
```




    California         NaN
    Ohio           70000.0
    Oregon         32000.0
    Texas         142000.0
    Utah               NaN
    dtype: float64




```python
#Series对象本身及其索引都有⼀个name属性，该属性跟pandas其他的关键功能关系⾮常密切
obj4.name = 'population'
obj4.index.name = 'state'
obj4
```




    state
    California        NaN
    Ohio          35000.0
    Oregon        16000.0
    Texas         71000.0
    Name: population, dtype: float64




```python
#Series的索引可以通过赋值改变
obj
```




    0    4
    1    7
    2   -5
    3    3
    dtype: int64




```python
obj.index = ['bob','steven','jeff','ryan']
obj
```




    bob       4
    steven    7
    jeff     -5
    ryan      3
    dtype: int64




```python
obj.index = ['bob','steven','jeff','ryan','rogen']
obj
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-23-9c0630cb4cf5> in <module>
    ----> 1 obj.index = ['bob','steven','jeff','ryan','rogen']
          2 obj
    

    ~\Anaconda3\lib\site-packages\pandas\core\generic.py in __setattr__(self, name, value)
       5190         try:
       5191             object.__getattribute__(self, name)
    -> 5192             return object.__setattr__(self, name, value)
       5193         except AttributeError:
       5194             pass
    

    pandas\_libs\properties.pyx in pandas._libs.properties.AxisProperty.__set__()
    

    ~\Anaconda3\lib\site-packages\pandas\core\series.py in _set_axis(self, axis, labels, fastpath)
        439         object.__setattr__(self, "_index", labels)
        440         if not fastpath:
    --> 441             self._data.set_axis(axis, labels)
        442 
        443     def _set_subtyp(self, is_all_dates):
    

    ~\Anaconda3\lib\site-packages\pandas\core\internals\managers.py in set_axis(self, axis, new_labels)
        181             raise ValueError(
        182                 "Length mismatch: Expected axis has {old} elements, new "
    --> 183                 "values have {new} elements".format(old=old_len, new=new_len)
        184             )
        185 
    

    ValueError: Length mismatch: Expected axis has 4 elements, new values have 5 elements



```python

```
