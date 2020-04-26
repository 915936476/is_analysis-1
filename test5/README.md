
# 实验5：图书管理系统数据库设计与界面设计
|学号|班级|姓名|
|:-------:|:-------------: | :----------:|
|2017104141102|软件(本)17-1|陈珏岷|

## 1.数据库表设计

## 1.1. 书籍信息表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|book_id|int(8)|主键|否|||书籍编号|
|book_name|varchar(20)| |否|||书籍名称|
|book_author|varchar(5)| |否|||书籍作者|
|book_pub|varchar(20)| |否|||书籍出版社|
|book_num|int(4)| |是|||当前库存数量|
|book_record|dateTime| |是|||书籍登记日期|
|book_type|varchar(20)| |是|||图书分类|

## 1.2. 读者信息表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|reader_id|varchar(20)|主键|否|||读者编号|
|reader_name|varchar(5)| |否|||读者姓名|
|reader_sex|varchar(2)| |否|||读者性别|
|reader_num|varchar(100)| |否|||读者学号|
|reader_dep|varchar(100)| |可|||读者所在学院|
|reader_pref|char| |可|||读者所属专业|
|reader_grade|char| |可|||读者的年级|
|reader_reg|dateTime| |可|||办证日期|
|id_select|int(1)||否|||用户识别号|


## 1.3. 管理员信息表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|manager_ID|varchar2(100)|主键|否|||管理员编号|
|manager_name|varchar2(100)| |否|||管理员姓名|
|manager_sex|varchar2(100)| |否|||管理员性别|
|manager_psw|varchar2(100)| |否|||管理员密码|
|manager_auth|varchar2(100)| |否|||管理员权限|
|id_select|int(1)||否|||用户识别号|

## 1.4. 学生借阅信息登记表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|save_id|int(8)|主键|否|||借阅记录编号|
|book_id|int(8)|外键|否|||书籍编号|
|read_id|varchar(20)|外键|否|||读者编号|
|borrow_date|datetime| |否|||借书时间|
|except_return_date|datetime| |否|||预期归还时间|
|return_date_count|int(5)| |是|||距离归还时间|
|return_date|datetime| |是|||实际还书时间|
|over_date|int(100)| |是|||超期天数|
|ticket_fee|float| |是|||处罚金额|


## 1.5. 读者借书请求管理表
|字段|类型|主键，外键|可以为空|默认值|约束|说明|
|:-------:|:-------------:|:------:|:----:|:---:|:----:|:-----|
|read_id|varchar(20)|主键|否|||读者编号|
|max_num|varchar(100)| |否|||允许借阅图书最大数|
|max_day|varchar(100)| |否|||持有图书最长期限|
|max_idcard_date|varchar(100)| |否|||借阅证期限|


***
<br>
<br>
<br>

## 2. 界面设计
## 2.1. 读者登陆界面设计
https://Chenjuemin.github.io/is_analysis_pages/登陆页面.html</br>
- 用例图参见：登陆用例
- 类图参见：管理员类，读者类
- 顺序图参见：login()
- API接口如下：  
<br>

1.登陆
- 功能：登陆用户
- 请求地址： http://mybook/v1/api/login
- 请求方法：GET
- 请求参数：

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|rule_take|是|用于验证请求合法性的认证信息。 |
|method|是|固定为 “GET”。|

- 返回实例：
```
{
    "user": "username，password",
    “seclet—id”："1"
    "code": 200
}
```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|user|返回类型为user的登陆对象的信息|
|code|返回码|
|seclet—id|1为普通用户，2为管理员|
---
<br>
<br>
<br>

## 2.2. 读者界面设计
https://Chenjuemin.github.io/is_analysis_pages/读者界面.html</br>
- 类图参见：读者类，图书类
- 顺序图参见：所有读者顺序图起始，读者借阅顺序图
- API接口如下：

1. 获取个人简易借阅情况
- 功能：获取个人借阅情况
- 请求地址： http://mybook/v1/api/user
- 请求方法：PUT
- 请求参数：

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|rule_take|是|用于验证请求合法性的认证信息。 |
|method|是|PUT|

- 返回实例：
```
{
    "info": "获取借阅情况",
    "data": {
        "book_id": "10045",
        "book_name": "爱的教育",
        "return_date_count": "9天",
      }
    "code": 200
}
```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|info|返回信息|
|book_id|书籍编号|
|book_name|书籍名称|
|return_date_count|预计归还时间剩余|
|code|返回码|





## 2.3.书籍预约界面设计
https://chenjuemin.github.io/is_analysis_pages/借书界面.html</br>
- 用例图参见：书籍预约用例
- 类图参见：读者类，图书类
- 顺序图参见：预约书籍
- API接口如下：

1. 书籍预约
- 功能：借阅书籍
- 请求地址： http://mybook/v1/api/bookappointment
- 请求方法：PUT
- 请求参数：

|参数名称|必填|说明|
|:-------:|:-------------: | :----------:|
|rule_take|是|用于验证请求合法性的认证信息。 |
|method|是|PUT|

- 返回实例：
```
{
    "info": "借阅书籍",
    "data": {
        "read_id": "188289",
        "read_name": "小明",
        "book_id": "000011",
        "book_name": "时间简史",
        "borrow_date": "2020.1.20",
        "except_return_date": "2020.2.20",
      }
       
    "code": 200
}
```
- 返回参数说明：
    
|参数名称|说明|
|:-------:|:-------------: |
|Info|借阅书籍|
|reader_id|读者id|
|reader_name|读者名称|
|book_id|书籍id|
|book_name|书籍名称|
|borrow_date|书籍借阅日期|
|except_return_date|预期书籍归还日期|
|code|返回码|

