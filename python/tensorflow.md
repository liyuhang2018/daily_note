##　 tf.name_scope对tf.get_variable()的影响

###  用var2来初始化var1  //复制值

```python
var1 = tf.get_variable(name='var1', shape=[1], dtype=tf.float32, initializer=initializer)

var2 = tf.get_variable(name='var2', dtype=tf.float32, initializer=var1)


#变量名称只是指针名，变量的name是地址

#虽然variable_scope可以增加name“范围”，但是get_variable取值的唯一性仍旧需要维护，否则就会出错，你是不可以任性新建的。那我现在就是想重用此变量，我就是想更改一个变量名而已，行吗？当然行，之前我们就采用了直接变量名赋值就行了“var3=var1”，这样变量名改为了var3，但是其name仍旧是var1的name，从c理解就是，指针随便建，地址唯一不变，街道名你随便改，可是街道你不能随便拆改。那还有一种材料中介绍的方法，就是使用reuse_variables(),但是一旦重用的对象本身不存在就会报错。这里说的对象不是“指针”，而是指针地址，而且是带有variable_scope指定的“范围”的指针地址。

```

### var1改个名

```
var3 = var1
```

## variable_scope对get_variable的影响　

1]. name_scope 对 get_variable新建变量的name属性无影响；对variable新建变量的name属性增加了“范围”标识。

[2]. variable_scope对get_variable新建变量的name属性和variable新建变量的name属性都增加了“范围”标识。

[3]. get_variable新建变量如果遇见重复的name则会因为重复而报错。

[4]. variable新建的变量如果遇见重复的name则会自动修改前缀，以避免重复出现。

```python
with tf.variable_scope("foo"):
    v2 = tf.get_variable("v",[1])

v1 = tf.get_variable("v",[1])

print(v1.name)
v:0

    
    
print(v2.name)
foo/v:0

    
    
with tf.variable_scope("foo",reuse=True):
    v3 = tf.get_variable("v",[1])
print(v3.name)
foo/v:0
```

关于collection

```
在tf.ged_tvariable(collection = [avc,tf.Graphkeys..])
说明把这个变量存到avc和tf.Graphkeys中

然后可以tf.get_collection得到它
```

## TensorFlow - tf.multiply和tf.matmul 区别

```python
# a
# [[1, 2, 3],
#  [4, 5, 6]] a = tf.constant([1, 2, 3, 4, 5, 6], shape=[2, 3])

# b1
# [[ 7,  8],
#  [ 9, 10],
#  [11, 12]] b1 = tf.constant([7, 8, 9, 10, 11, 12], shape=[3, 2])

#b2
#[[ 7  8  9]
# [10 11 12]] b2 = tf.constant([7, 8, 9, 10, 11, 12], shape=[2, 3])


# c矩阵相乘 第一个矩阵的列数（column）等于第二个矩阵的行数（row）
# [[ 58,  64],
#  [139, 154]] c = tf.matmul(a, b1)

# d`数元素各自相乘
#[[ 7 16 27]
# [40 55 72]] d = tf.multiply(a, b2) #维度必须相等 with tf.Session():
    print(d.eval())

```

```python
b3 = tf.constant([7, 8, 9,], shape=[1, 3])
tf.multiply(a, b3)
结果是
[[ 7 16 27]
 [28 40 54]]


b4 = tf.constant([7, 8], shape=[2, 1])
tf.multiply(a, b4)
结果是
[[ 7 14 21]
 [32 40 48]]

b5 = tf.constant([7], shape=[1, 1])
tf.multiply(a, b5)
结果是
[[ 7 14 21]
 [28 35 42]]

```

