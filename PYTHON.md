# PYTHON基础

## 一:运算符

| 运算符                      | 描述                        |
| --------------------------- | --------------------------- |
| **                          | 指数                        |
| ~ + -                       | 按位取反,正负号             |
| * / % //                    | 乘,除,模,整除               |
| + -                         | 加,减                       |
| >> <<                       | 右移,左移                   |
| & ^ \|                      | 按位与,按位异或,按位或      |
| <= < > >=                   | 小于等于 小于 大于 大于等于 |
| ==  ！=                     | 等于 ,不等于                |
| is is not                   | 身份运算符                  |
| in not in                   | 成员运算符                  |
| not or and                  | 逻辑运算符                  |
| [] [:]                      | 下标运算符                  |
| = += -= *= /+ %= //= **= &= | =` `^=` `>>=` `<<=`         |
|                             |                             |

举例1

```python
"""
经常遗忘的举例

version 1.0
authon 华
"""
a = 2
b = 5
print(a/b) #0.4  除
print(a//b) #0   整除           通常//10取前n-1位
print(a%b) #2    取余数 负数同理  通常%10取最后一位
print(a>>b) #0   右移   10右移一位为1
print(a<<b) #64   左移 相当于 a*2**b a乘以2的b次方  10左移一位为100
print(a&b) #0  10和101按位与为0  同时为1则为1,否则为0
print(a|b) #7  10和101按位或为 111 有一个为1则为1 十进制为7
print(a^b) #7   10和101按位或为 111 相同为0，不同为1 十进制为7

#----------------------摄氏温度和华氏温度转换--------
f = float(input('请输入华氏温度：'))
c = (f - 32) /1.8
print('%.1f华氏度 = %。1f摄氏度' %(f,c))
#----------------------判断年份是不是闰年------------
year = int(input('请输入年份:'))
is_leap = (year % 4 == 0 and year % 100 !=0) or year % 400 ==0
```

注:左移和右移运算,先把十进制数转成二进制数,左移全部往前移动一位,后面补0.右移为全部往后移动一位,把最右面的一位去掉。然后再转换为十进制

## 二:分支

嵌套和扁平化

```python
"""
分段函数求值
       x- 1 (x>1)  
f(x) = 2x + 1(-1<=x <=1)
       x*7 -9(x<-1)
"""
x = float(intput('x = '))
if x >1:
    y = x-1
elif x>= -1 and x <=1:
    y = 2x+1
else:
    y = x*7 -9
#---------嵌套写法(可读性差)--
if x >1:
    y = x -1
else:
    if x >=-1:
        y = 2x+1
    else:
        y = x*7 -9
#-----英寸与厘米相互转化
value = float(input('请输入长度:'))
unit = input('请输入单位')
if unit =='in' or unit == '厘米':
    print('%f英寸 = %f厘米' %(value,value*2.54))
elif unit =='cm' or unit == '厘米':
    print('%f厘米 = %f英寸'%(value,value/2.54))
else:
    print('请输入有效单位')
```

## 三:循环

在python中构造循环一般有两种写法,for-in和while

### for-in

```python
"""
version 1.0
求0-100的和
"""
for x in range(101):
    sum+=x
print(sum)
```

- range(101) 0-100的整数数列
- range(1,100) 1-99的整数数列
- range(1,100,2) 1-99的奇数数列 

```python
"""
version 1.0
获取列表元素和下表
"""
alp = ['a','b','c']
for index,value in enumerate(alp):
    print(index,value)
```

### while

```python
"""
version 1.0
猜数字
"""
import random
answer = random.randint(1,100)
counter = 0
while True:
    counter+=1
    number = int(input('请输入'))
    if number < answer:
        print('大一点')
    elif number > answer:
        print('小一点')
    else:
        print('猜对了')
        break
        
```

break和continue,break结束本次循环,continue跳过本次循环进入下一次循环

```python
"""
version 1.0
break 和continue
"""
for x in range(3):
    if(x == 1):
        break
    print(x) #0
#----
for x in range(3):
    if(x == 1):
        continue
    print(x) #0,2
```

## 四:函数

例子

```python
"""
version 1.0
"""
def function(x,y):
    (x,y) = (y,x) if x>y else (x,y)
    for factor in range(x,0,-1):
        if x % factor == 0 and y % factor == 0:
            return factor,x*y //factor

```

函数参数

```python
"""
version 1.0
"""
#1
def func1(arg):
    pass
#2
def func2(arg1,arg2=3):
    pass
#3
def func3(arg1,*arg2):
    pass
#4
def func4(arg1,**arg2):
    pass


aa = {'name':'hua','age':18}
bb = (1,2,3,4,5)
def func(arg1,arg2,*arg3,**arg4):
    print(arg1,arg2,arg3,arg4)
func(1,2,bb,aa)
#1 2 (1, 2, 3, 4, 5) {'name': 'hua', 'age': 18}

```

作用域

```python
"""
veriosn 1.0
"""
def func1():
    global a = 9
    b = 1
    def func2():
        c=2
        print(a)
        print(b)
        print(c)
    func2()
if __name__ == '__main__':
    a = 4
    #b,c没有定义
    func1() #可以输出a,b,c a不能被修改,若要修改,需要加global关键字

```

## 五:数据结构

### 转义

可以在字符串中使用\\(反斜杠)来表示转义,如\\n表示换行,\\t表示制表符

s1 = '\n\\hello,world!\\\n'

在\\后面可以跟一个八进制或者十六进制数来表示字符

\\141 \\x61都表示a

在\\后面可以跟Unicode字符编码来表示字符

如果不希望字符串中的\\表示转义,可以在字符串的最前面加上字母r

s1 =  r'\n\\hello,world!\\\n'

### 字符串运算

```python
"""
version 1.0 
常用字符串操作
"""
s1 = 'nihao'*3
print(s1) #nihao nihao nihao
s2 = 'haha'
s1+=s2
print(s1) #nihao nihao nihao nihao haha
print('ha' in s1) #True
print('aa' in s1) #False
str2 = 'qwert123'
print(str2[2]) #e
print(str2[2:4])#er
print(str2[2::2])#et2
print(str2[::2])#qet2
print(str2[::-1])#321trewq
print(str2[-3:-1])#12

#---------------字符串处理-----------
str = 'hello, world'
print(len(str))#13
print(str.capitalize) #Hello ,world
print(str.title)#Hello,World
print(str.upper())#HELLO ,WORLD
print(str.find('or'))#8
print(str.find('shit'))#-1
print(str.isdigit())#False
print(str.isalpha())#True
print(str.isalnum())#False
print(str.strip())


```

#### 格式化输出

```python
"""
version 1.0
格式化输出三种方式
"""
a,b =1,2

print('%d * %d = %d'%(a,b,a*b))
print('{0} * {1} = {2}'.format(a,b,a*b))
print(f'{a} * {b} ={a*b}')


```

### 列表操作

```python
"""
version 1.0
列表常用操作
"""
list1 = [1,2,3,4,5]
#列表元素
for index in range(len(list1)):
    print(list1[index])
for elem in list1:
    print(elem)
for index,elem in enumerate(list1):
    print(index,elem)
    
#添加元素
list1.append(90)
list1.insert(1,66)

#合并列表
list1+=[100,200]
#移除
if 3 in list1:
    list1.remove(3)
list1.pop(0)
#清空
list1.clear()

#排序
list2 = sorted(list1,key=len) #根据长度进行排序


```

#### 生成式和生成器

```python
"""
version 1.0
"""
#生成式
f = [x for x in range(1,10)]
f = [x + y for x in 'abcd' for y in '123456']
f = [x ** 2 for x in range(1,1000)]
print(sys.getsizeof(f))#4516 通过列表生成式语法会消耗内存空间

#生成器
f = (x ** 2 for x in range(1,1000))
print(sys.getsizeof(f))#48 通过列表生成器语法不会占用存储数据的空间


#yield
def aa():
	for x in range(4):
		yield x
print(list(aa()))#0,1,2,3

```

## 元组

特点:

1.元组中元素是无法修改的,不需要对元素进行增删改,可以使用元组,是线程安全的

2.元组在创建时间和占用空间上优于列表

```python
"""
version 1.0
"""
t = ('hua',18,'新乡')
print(t[0])#hua
for value in t:
    print(value)
t[0] = 'haha'#TypeError: 'tuple' object does not support item assignment
print(list(t))#元组转列表

l = ['i','love','you']
print(tuple(l))#列表转成元组
```

## 集合

特点:元素不能重复,可以进行交并差运算

```python
"""
version 1.0
创建集合的几种方法
"""
#字面量语法
s = {1,2,3,4,5,6,7}
#构造器语法
s = set(range(1,10))
s = set((1,2,3,4,5,6))
#推导式语法
s = {num for num in range(1,100) if num %3 ==0}
```

```python
"""
version 1.0
集合运算
"""
s.add(9)
s.update([8,7]) #元素按顺序排列
s.discard(4)#删除元素
s.pop()
#---------------交并差运算--------
s1 = {7,2,3,4}
s2 = {4,5,6,7}
#交集
print(s1 & s2)#{4，7}
print(s1.intersection(s2))
#并集
print(s1 | s2)#{2, 3, 4, 5, 6, 7}
print(s1.union(s2))
#差集
print(s1 - s2) #{2,3}
print(s1.difference(s2))
#对称差运算   -- 取两个集合全部不一样的 相当于(s1 - s2) | (s2 - s1)
print(s1 ^ s2) #{2,3,5,6}
print(s1.symmetric_difference(s2))

#判断子集和超集
print(s1 <= s2) #False
print(s1.issubset(s2))

print(s1>=s2)#False
print(s1.issuperset(s2))


```

## 字典

```python
"""
version 1.0
创建字典的几种方式
"""
#字面量语法
person = {'name':'hua','age':18}
#构造器语法
person = dict(name = 'hua',age = 18)
#zip函数
person = dict(zip(['a','b','c'],'456'))
#推导式语法
person = {x:x**2 for x in range(1,9)}
```

```python
"""
version 1.0
字典常用操作
"""
print(person['name'])
for key in person:
    print(f'{key}:{person[key]}')

person['name'] = 'haha'
person.get('name')
person.update(address = 'xinxiang')
person.popitem()
person.pop('name')
person.clear()
```





例子:约瑟夫环问题

```python
"""
version 1.0
《幸运的基督徒》
有15个基督徒和15个非基督徒在海上遇险，为了能让一部分人活下来不得不将其中15个人扔到海里面去，有个人想了个办法就是大家围成一个圈，由某个人开始从1报数，报到9的人就扔到海里面，他后面的人接着从1开始报数，报到9的人继续扔到海里面，直到扔掉15个人。由于上帝的保佑，15个基督徒都幸免于难，问这些人最开始是怎么站的，哪些位置是基督徒哪些位置是非基督徒。
"""
def main():
    persons = [True]*30
    counter,index,number = 0,0,0
    while counter < 15:
        if persons[index]:
            number +=1
            if number == 9:
                person[index] = False
                counter +=1
                number = 0
        index +=1
        index %= 30
    for person in persons:
        print('基' if person else '非',end = '')

```

# 六:面向对象

ddd

