# 财务系统设计相关

## 金额计算

使用

update account set amount = amount + out/in

避免使用

select amount from account

$amount = amount + out/in

update account set amount = $amount