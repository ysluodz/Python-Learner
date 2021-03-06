* 文件读取

```python
###1.python  
#读写txt
with open(r'./data/user_dict.txt','r',encoding='utf-8') as f:
    data = f.readlines()
#追加模式
with open(r'./data/user_dict.txt','a',encoding='utf-8') as f:
    t = '你好'
    f.write('\n'+t)

#按行读取tsv / 内存大可以直接.readlines()
with open('./data/train.tsv',encoding = 'utf-8') as file:
    line = file.readline()
    limit = 0
    while line and limit<10:
        print(line)
        limit+=1
        line = file.readline()

###2.json 存储dict
x = {..}
#save
with open(r"./x.json",'w') as f:  
    json.dump(x, f, ensure_ascii=False)     
print('done')
#read
with open(r"./x.json",'r') as f:
    for line in f:
        x = json.loads(line)  

###3.numpy 存储list
x = [x,]
np.save("./././x.npy",x)
x = np.load(r"./././x.npy")

###4.pandas
#read xlsx
data = pd.read_excel(r'xxxx.xlsx','Sheet1')

#dict to df
result = {x:1,y:2,..}  
df = pd.DataFrame(list(result.items()), columns=['key','value'])
#save df
df.to_csv(r"./result.csv", index=False,header=True)
#read
df = pd.read_csv(r'./result.csv',encoding = 'gbk')
```

* 字符串判断

```pyhton
s.islower() #判断是否所有字符小写
s.isupper() #判断是否所有字符大写
s.isalpha() #判断是否所有字符为字母
s.isalnum() #判断是否所有字符为字母或数字
s.isdigit() #判断是否所有字符为数字
s.istitle() #判断是否所有字符为首字母大写
```

* 统计list元素出现次数

```PYHTON
from collections import Counter
x = [1,2,3,2]
y= '1232'
Counter(x)
#>>Counter({2: 2, 1: 1, 3: 1})  #就是一个dict
Counter(y)
#>>Counter({'2': 2, '1': 1, '3': 1})
Counter('1232')['2']
#>>2
```

* timestamp 转换标准时间
```
# 把时间处理 以找到登陆时间
import time
def timestamp_datetime(value):
    format = '%Y-%m-%d %H:%M:%S'
 # value为传入的值为时间戳(整形)，如：1332888820
    value = time.localtime(value)
 ## 经过localtime转换后变成
 ## time.struct_time(tm_year=2012, tm_mon=3, tm_mday=28, tm_hour=6, tm_min=53, tm_sec=40, tm_wday=2, tm_yday=88, tm_isdst=0)
 # 最后再经过strftime函数转换为正常日期格式。
    dt = time.strftime(format, value)
    return dt
def datetime_timestamp(dt):
  #dt为字符串
  #中间过程，一般都需要将字符串转化为时间数组
    time.strptime(dt, '%Y-%m-%d %H:%M:%S')
  ## time.struct_time(tm_year=2012, tm_mon=3, tm_mday=28, tm_hour=6, tm_min=53, tm_sec=40, tm_wday=2, tm_yday=88, tm_isdst=-1)
  #将"2012-03-28 06:53:40"转化为时间戳
    s = time.mktime(time.strptime(dt, '%Y-%m-%d %H:%M:%S'))
    return int(s)

d = datetime_timestamp('2015-03-30 16:38:20')
print(d)
s = timestamp_datetime(1427704700)
print(s)
```

* 排序
```
#方法1.用List的成员函数sort进行排序，在本地进行排序，不返回副本
#方法2.用built-in函数sorted进行排序（从2.4开始），返回副本，原始输入不变
listX = [[1,4],[2,5],[3,3]]
sorted(listX, key=lambda x : x[1])
#>>[[3, 3], [1, 4], [2, 5]]
```
