###权限和登录

1. 登录

   请求示例

   ```json
   {"mobile":"15500000000","password":"111111"}
   ```

   

   返回结果(登录成功)

   > status: 200

   ```json
   {
       "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9xaWFuZGFvLm9vXC9hcGlcL2FkbWluXC9sb2dpbiIsImlhdCI6MTUyNTUwNDA3MywiZXhwIjoxNTI5MTA0MDczLCJuYmYiOjE1MjU1MDQwNzMsImp0aSI6ImNMQzdXOUpFeUhMYUNCR1ciLCJzdWIiOjEsInBydiI6ImIyN2JlZTIzYmFmNTQyOWY1YjlhMjE2OTZmZGUwM2MyNzcwNDRlYTUifQ.Zcj-dPU-APsqUJSrEwbalTTI9SqeiJyuKkM2xWETBBg",
       "token_type": "bearer",
       "expires_in": 3600000
   }
   ```

   | 字段         | 函义     |
   | ------------ | -------- |
   | access_token | 访问令牌 |
   | token_type   | 加密方式 |
   | expires_in   | 有效时长 |

   返回结果登录失败

   > status: 401

   ```json
   {"error": "Unauthorized."}
   ```

2.  在请求头部加入令牌

   ```javascript
   // 单个请求
   let token_str = '{"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9xaWFuZGFvLm9vXC9hcGlcL2FkbWluXC9sb2dpbiIsImlhdCI6MTUyNTUwNDA3MywiZXhwIjoxNTI5MTA0MDczLCJuYmYiOjE1MjU1MDQwNzMsImp0aSI6ImNMQzdXOUpFeUhMYUNCR1ciLCJzdWIiOjEsInBydiI6ImIyN2JlZTIzYmFmNTQyOWY1YjlhMjE2OTZmZGUwM2MyNzcwNDRlYTUifQ.Zcj-dPU-APsqUJSrEwbalTTI9SqeiJyuKkM2xWETBBg","token_type": "bearer","expires_in": 3600000}';
   let token = JSON.parse(token_str);
   
   // jquery 单个请求
   $.ajax({
       type: 'POST',
       url: '/request',
       headers: { Authorization: `${token.bear} ${token.access_token}` },
       data: "{}"
   });
   
   // jquery 全局头
   $.ajaxSetup({
       headers: { Authorization: `${token.bear} ${token.access_token}` },
   })
   
   // axios
   
   // fetch
   
   let headers = new Headers();
   // headers.append('Accept', 'application/json'); 
   headers.append('Authorization', `${token.bear} ${token.access_token}`); 
   let request = new Request(URL, {
       headers: headers,
       method:"GET"
   });
   fetch(request).then(function(response) { 
       console.log(response);
   });
   
   ```

3.  令牌缺失或失效请求示例

   > status 401

   ```json
   {"error": "Unauthorized."}
   ```

   

4. 权限(访问禁止访问的资源)

   > status 403

   ```json
   {"error": "对不起，您没有访问权限"}
   ```

   

   


### 数据获取

1. 带分页的接口

   返回示例

   ```json
   {
       "current_page": 1,
       "first_page_url": "http://qiandao.oo/api/admin/activity?page=1",
       "from": 1,
       "last_page": 1,
       "last_page_url": "http://qiandao.oo/api/admin/activity?page=1",
       "next_page_url": null,
       "path": "http://qiandao.oo/api/admin/activity",
       "per_page": 15,
       "prev_page_url": null,
       "to": 3,
       "total": 3,
       "data": [ ... ]
   }
   ```

| 字段          | 含义                                         |
| ------------- | -------------------------------------------- |
| current_page  | 当前页码                                     |
| data          | 数据列表(数组[])                             |
| from          | 返回数据中第一条数据在查询中的排序位置       |
| to            | 返回数据中最后一条的在查询中的排序位置       |
| last_page     | 最后一页的页码                               |
| last_page_url | 最后一页的链接                               |
| next_page_url | 下一页的链接                                 |
| path          | 不带页码的请求链接，不带参数返回第一页的数据 |
| per_page      | 每页条数                                     |



### 填充和修改

