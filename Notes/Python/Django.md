# Django

## Installation

假设已经安装python

### By pip

`pip3 install Django`

## 运行

django-admin startproject mysite

python3 manage.py runserver

python3 manage.py startapp polls

## 数据库配置

<https://docs.djangoproject.com/zh-hans/2.0/intro/tutorial02/>

python3 manage.py migrate

## 问题

1. 出现`Symbol not found: _sqlite3_enable_load_extension`

brew install sqlite

brew upgrage