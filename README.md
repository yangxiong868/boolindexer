# boolindexer
boolindexer 是一个用于检索bool 表达式的库， 具体的实现原理可以参照论文 [Indexing Boolean Expressions](http://theory.stanford.edu/~sergei/papers/vldb09-indexing.pdf)

## DNF(Disjunctive Normal Form)
DNF 即析取范式， 由不同的逻辑表达式 通过 "与"组成。 每个逻辑表达式内部，可以是或， 或者是否
例如：
年龄∈[1,2,3] & 性别∈[男] & 爱好∈[篮球] & 地域∉[上海]

其中 年龄∈[1,2,3] , 性别∈[男] ,  爱好∈[篮球] , 地域∉[上海] 称之为assignment
每个assignment 由若干个term组成。 
term 可以视作是一个最小的key, value集合
例如 : 年龄∈[1,2,3] ， 可分解为<年龄，1>, <年龄，2>,<年龄，3>
assignment 的另一个属性为 属于或者不属于
对于 地域∉[上海]， 它就是不属于

## 构建索引
构建索引， 需要输入文档信息。 每个文档由若干的属性组成
比如： 
文档1,  地域∈[上海, 北京] & 年龄 ∈[20, 25]
文档2， 地域∈[南京] & 年龄 ∈[30,40] & 性别 ∈[男]
根据文档的属性， 建立倒排索引， 用于检索

## 检索
输入若干个属性的条件，获取符合该条件的文件
例如条件为： 年龄=30 & 性别 = 男， 输出 文档集合

## 应用
bool表达式的检索， 最典型的应用场景就是互联网广告的定向过滤。 
广告主在投单的时候， 会设置很多的定向条件。 当一个流量过来时， 怎么在最短的时间内匹配出合适的广告， 就可以使用该项目中使用的算法
