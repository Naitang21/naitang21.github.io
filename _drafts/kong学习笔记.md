## Kong是什么
Api网关，用于处理HTTP和HTTPS的请求，建立在Nginx HTTP服务器之上，通过Lua语言的插件拓展其功能



## Kong-config
```
_format_version: "2.1"  
_transform: true

// 最终用户或服务的主体，使用我们暴露出去的API的service或client
consumers: 
- username: 
  custom_id:

services:
- name: API所在的service
url: API的url
routes:  
- name: API的路由名称
  paths:  
  - API路径，比如"/xxx/xxxx/xxxxxx"
  methods:["POST"]

plugins:  
- name: plugin-name
  config:  
    path: 比如”/xxx/xxx“

```

service可以和route关联，一个service可以有很多route。

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwMDU5NDUxMl19
-->