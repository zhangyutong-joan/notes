# 深度学习/数据分析中一些常见函数
**squeeze()：** 所有长度为1的维度都会被移除

- squeeze(0)：删去第0个维度

## numpy的一些常见函数
**np.vstack()**：按垂直方向（行顺序）堆叠数组构成一个新的数组

*堆叠的数组需要具有相同的维度*

```
a=np.array([[1,2,3]])
b=np.array([[3,4,5]])
c=np.vstack((a,b))
# array([[1,2,3], 
         [3,4,5]  ])
```

**np.hstack()**：按水平方向堆叠

```
a=np.array([1,2,3])
b=np.array([0] * 10)
c=np.hstack((a,b))# array([1, 2, 3, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0])
```

## torch的一些常见函数
**x.view()：** 就是对tensor进行reshape。

## pandas的一些常见函数
**reset_index**<br />
DataFrame.reset_index(self, level=None, drop=False, inplace=False, col_level=0, col_fill='') 
- drop: 如果将该参数设置为True，则会将原来的索引丢弃，不作为新的列添加到DataFrame中。默认为False。

**sort_values**<br />
DataFrame.sort_values(by, axis=0, ascending=True, inplace=False, kind='quicksort', na_position='last', ignore_index=False, key=None) 
- ignore_index: 如果为 True，重置索引。默认为 False。

**to_sql**<br />
在python3中，to_sql()的con对象，是 sqlalchemy 的 engine 引擎，通过sqlalchemy的create_engine创建：
```
engine = create_engine('mysql+mysqldb://user:passwd@127.0.0.1/database?charset=utf8') # 或
engine = create_engine('mysql+mysqlconnector:// user:passwd@127.0.0.1/database?charset=utf8') 
# 用户名:密码@服务器地址/数据库名
```
df.to_sql(name, con, schema=None, if_exists='fail', index=True, index_label=None, chunksize=None, dtype=None, method=None)
- **if_exists**：当数据库中已经存在数据表时对数据表的操作，有replace替换、append追加，fail则当表存在时提示ValueError。
- **index**：对DataFrame的index索引的处理，为True时索引也将作为数据写入数据表
- **index_label**：当上一个参数index为True时，设置写入数据表时index的列名称
- **chunsize**：设置整数，如20000，一次写入数据时的数据行数量，**当数据量很大时，需要设置，否则会链接超时写入失败。**
- **dtype**：写入数据表时，可以设置列的名称(The keys should be the column
names and the values should be the SQLAlchemy types or strings for
the sqlite3 legacy mode),需要设置时，类型需要和sqlalchemy的类型保持一致.当不设置时，to_sql生成表时会自动兼容最大的类型。
可以设置的数据类型有：
 [‘TypeEngine’, ‘TypeDecorator’, ‘UserDefinedType’, ‘INT’, ‘CHAR’, ‘VARCHAR’, ‘NCHAR’, ‘NVARCHAR’, ‘TEXT’, ‘Text’, ‘FLOAT’, ‘NUMERIC’, ‘REAL’, ‘DECIMAL’, ‘TIMESTAMP’, ‘DATETIME’, ‘CLOB’, ‘BLOB’, ‘BINARY’, ‘VARBINARY’, ‘BOOLEAN’, ‘BIGINT’, ‘SMALLINT’, ‘INTEGER’, ‘DATE’, ‘TIME’, ‘String’, ‘Integer’, ‘SmallInteger’, ‘BigInteger’, ‘Numeric’, ‘Float’, ‘DateTime’, ‘Date’, ‘Time’, ‘LargeBinary’, ‘Binary’, ‘Boolean’, ‘Unicode’, ‘Concatenable’, ‘UnicodeText’, ‘PickleType’, ‘Interval’, ‘Enum’, ‘Indexable’, ‘ARRAY’, ‘JSON’] 
 <br /> 示例<br />
 
```
from sqlalchemy.types import DATE,CHAR,VARCHAR 
DTYPES = {'col_1字段名称' : DATE, 'col_2':CHAR(4),'col_3':VARCHAR(10)}
df.to_sql(....,dtype = DTYPES)
```