# 财务系统设计相关

### 金额计算

使用

update account set amount = amount + out/in

避免使用

select amount from account

$amount = amount + out/in

update account set amount = $amount

### 保留原始流水数据

对于财务操作中的流水，包括转账、还款、冲销等等，一定要保存好最原始的所有明细数据，

还款计划则另外保存，分离设计，确保在数据调整后，也能完整的重现整个过程。