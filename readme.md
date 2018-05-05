##权限和登录

## 数据获取

1. 带分页的接口

![带分页的接口](.\img\TIM图片20180505145446.png)

| 字段          | 含义                                         |      |
| ------------- | -------------------------------------------- | ---- |
| current_page  | 当前页码                                     |      |
| data          | 数据列表(数组[])                             |      |
| from          | 返回数据中第一条数据在查询中的排序位置       |      |
| to            | 返回数据中最后一条的在查询中的排序位置       |      |
| last_page     | 最后一页的页码                               |      |
| last_page_url | 最后一页的链接                               |      |
| next_page_url | 下一页的链接                                 |      |
| path          | 不带页码的请求链接，不带参数返回第一页的数据 |      |
| per_page      | 每页条数                                     |      |
| prev_page     | 上一页的页码                                 |      |
| prev_page_url | 上一页我链接                                 |      |
| total         | 数据总条数                                   |      |







## 填充和修改
