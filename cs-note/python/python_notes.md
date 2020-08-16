# Python笔记

## 《python编程从入门到实践》
### 基本
* 应使用英文小写的作为变量名
* 同时剔除字符串两端空白：strip()
* 两个乘号表示乘方运算
* python2整数除法的结果只包含整数部分，小数部分被删除。
### 列表删除元素
* 根据索引：
	* 使用del来删除元素，如 del list[1]
	* 使用pop()可删除列表的元素，并返回。pop()缺省弹出最后一个，可以指定删除元素的索引。
* 根据值：
	* remove()，只删除第一个指定的值，不删除存在重复的待删元素。
### 列表排序
* sort()，永久排序。list().sort()
* sorted()，临时排序。sorted(lsit)
* reverse() 反转输出

### 列表其他
* list复制，可以采用切片复制 a=b[:]，这样创建新的副本而不是直接原列表。
* 判断列表空，直接if list()

### 字典：
* 遍历字典时，items()是复制每一对（k,v）；viewitems()是观察每一个对(k,v)，因此当字典改变时，观察的(k,v)会改变。
* 按顺序遍历键：sorted(dict().keys())

### 函数：
* 若想传递列表的副本（不改变原列表），可以使用list_name[:]切片复制
* 传递任意数量的实参def fun(\*arg)，实际上是创建一个arg空元组，并将收到的所有值都封装到这个元组上。
* 传递任意数量的关键字实参def fun(\*\*arg)，实际创建了一个arg空字典，并将收到的所有键值对封装到 这个字典上。调用如fun(a=123,b=33432)
* 函数名只使用小写字母和下划线。
* 用两个空行将相邻函数分开

### 类
* 类名：驼峰命名，首字母大写，不用下划线。
* 类的每个属性都必须有初始值，
* 实例名和模块名：采用小写格式，并在单词间加上下划线。
* 在类中，使用一个空行来分隔方法；模块中，使用两个空行来分隔类。先编写导入标准库模块的import 语句，再添加一个空行，然后编写导入你自己编写的模块的import 语句。
* 同时导入标准库中的模块和自己编写的模块时，当一个类的属性和方法越来越多时。可以将类的一部分作为一个独立的类提取出来，然后实例化这个类用作自己的属性。
* [了解标准库](https://pymotw.com/3/)

### 文件
* read() 到达文件末尾时返回一个空字符串，所以最后会多一个空行。read()读取这个文件的全部内容，并将其作为一个长长的字符串存储在变量。
* readlines()读取文件的每一个行，并存在一个列表上。
* Python只能将字符串写入文本文件。要将数值数据存储到文本文件中，必须先使用函数str() 将其转换为字符串格式。
* write()不会写入换行符

### 异常
* try-excpet-else：提供了两个重要的优点:避免让用户看到traceback;让程序能够继续分析能够找到的其他文件。
* 可在except语句中加入pass语句，这样失败时可以一声不吭。

### 存储数据
* json.dump()/json.load()

### matplotlib
* 设置刻度大小，plt.tick_params()
* plt.axis()设置坐标轴的取值范围， 要求提供四个值:x 和 y 坐标轴的最小值和最大值。如plt.axis([0, 1100, 0, 1100000])
* 隐藏坐标plt.axes().get_xaxis().set_visible(False)
* 当向plot()提供一系列数字时，它会假设第一个数据点的x坐标值为0，所以为了正确绘制图像，应该同时提供x值数据和y值数据。
* 散点图plt.scatter()
* 颜色渐变：plt.scatter(x_values, y_values, c=y_values, cmap=plt.cm.Blues, edgecolor='none', s=40)  其中c参数表示渐变点的顺序，cmap告诉plt使用哪种颜色映射。
* 保存图表：忽略图表周围空白，plt.savefig('squares_plot.png', bbox_inches='tight')， bbox_inches参数设置。
* figure() 用于指定图表的宽度、高度、分辨率和背景色。
* fig.autofmt_xdate()，若标签太长时，可以自动排列标签，使其不重叠

### Pygal
* [生成矢量图工具](http://www.pygal.org/en/stable/index.html)

### 其他
* 不确定某个键是否包含在字典中时，可使用方法dict.get() ，它在指定的键存在时返回与之相关联的值，并在指定的键不存在时返回你指定 的值。

* operator的itemgetter模块是定义一个函数，可以获取数据某个维度的值，通过该函数作用到对象上才能获取值。如一个列表存放着多个字典，按照字典中的comments来排序列表：sorted(submission_dicts, key=itemgetter('comments'), reverse=True)

###  下载
requests.get(url)



## datetime和time的一些事

1. `time.time()`返回的是Unix时间戳
2. `time.localtime`()返回的是一个struct_time的类，里面包含如（tm_year=xxx, tm_mon=xxx...）
3. `datetime.datetime.now()`是把`time.time()`返回的时间戳转换为一个人能容易看的datetime类型，如`2020-08-16 23:34:40.0909`。datetime类型可比较
4. `time.strftime(format[, t])` 将指定的struct_time(默认为当前时间)，根据指定的格式化***字符串输出***
5. `time.strptime()`把一个时间字符串按某种格式转换为struct_time
6. `datetime.strptime()`把一个时间字符串按某种格式转化为datetime类型和`datetime.strftime()`相反。
7. `datetime.formtimestamp(t)`把一个Unix时间戳转化成datetime类型。




