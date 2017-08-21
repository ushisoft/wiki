# 小记

## Tensor

张量，三个属性：名字（name）、维度（shape）、类型（type）

## 会话Session

##### 模式一

```python
sess = tf.Session()
sess.run(...)
sess.close()
```
明确调用sess.close()关闭会话，然而当程序异常退出时，会导致close方法得不到执行，而导致资源泄漏。

##### 模式二

```python
with tf.Session() as sess
    sess.run(...)
```
当上下文管理器退出时，会自动释放资源。

##### 默认会话

```python
sess = tf.Session()
with sess.as_default():
    print(result.eval())
```
等同于：

```python
sess = tf.Session()
print(sess.run(result))
print(result.eval(session = sess))
```
##### InteractiveSession

自动将生成的会话注册为默认会话

##### ConfigProto

会话配置：

```python
config = tf.ConfigProto(allow_soft_placement = True,
                        log_device_placement = True)
sess1 = tf.InteractiveSession(config = config)
sess2 = tf.Session(config = config)
```
可配置并行的线程数、GPU分配策略、运算超时时间等。

allow_soft_placement = True时，在一下任何一个条件成立时，GPU上的运算可以放到CPU上运行：

1. 运算无法在GPU上进行
2. 没有GPU资源（比如运算被指定在第一个GPU上，可是机器只有一个GPU）
3. 运算输入包含对CPU计算结果的引用

该参数默认False，为使得代码的移植性更强，在有GPU的环境下，一般会设置为True。

log_device_placement = True时，日志中会记录各个节点被安排在了哪台设备上，方便调试。而在生产环境，则设置为False以减少日志量。

## TensorFlow游乐场

http://playground.tensorflow.org

输入层

隐藏层

节点，神经元（neuron）

边？（weights）

分类问题的4个步骤

1. 提取特征向量
2. 定义神经网络结构（前向传播算法）
3. 通过训练数据，调整神经网络中参数的取值
4. 使用训练好的神经网络来预测未知数据

## 神经网络参数

TensorFlow随机数生成函数

| 函数名称                | 随机数分布                                  | 主要参数                    |
| ------------------- | -------------------------------------- | ----------------------- |
| tf.random_normal    | 正态分布                                   | 平均值、标准差、取值类型            |
| tf.truncated_normal | 正态分布，但如果随机出来的值偏离平均值超过2个标准差，那么这个数将会重新随机 | 平均值、标准差、取值类型            |
| tf.random_uniform   | 平均分布                                   | 最小、最大取值，取值类型            |
| tf.random_gamma     | Gamma分布                                | 形状参数alpha、尺度参数beta、取值类型 |

常数生成函数

tf.zeros

tf.ones

tf.fill

tf.constant

### 初始化变量

initializer

变量变多后，逐个执行会比较麻烦，使用

```python
init_op = tf.initialize_all_variables()
sess.run(init_op)
```
该函数同时会自动解决变量间的依赖关系。

声明变量时参数trainable = True，那么这个变量会被加入GraphKeys.TRAINABLE_VARIABLES集合。

#### placeholder

feed_dict