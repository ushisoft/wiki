# 保留字段

## id、gmt_created、gmt_modified

在所有表中都添加这三个字段，在做分表，或者otter数据备份时，都有作用。

同时要避免这三个字段与业务上的联系，举个例子：

在会员表中，如果业务上需要记录会员的申请时间，要另外新建一个字段，比如applied_time，避免使用gmt_created。

### 自增id与uuid的选择

https://www.zhihu.com/question/43500172?sort=created