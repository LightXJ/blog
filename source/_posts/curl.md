curl 命令主要用于发出网络请求、提取数据。支持HTTP/HTTPS、FTP/FTPS、RTSP、POP3/POP3S、SCP、IMAP/IMAPS等协议。

### 一、常用参数
1、常用命令参数

```
-I    状态码  http  
-o    抓取页面到一个文件中
-x    代理
-X    curl默认的http动作是GET 使用-X参数可以支持其他动作
-v    可以显示一次http通信的整个过程
-u    账号：密码
-s    silent  静音模式
```

2、指定请求方法
```
-X POST 使用post方法，当使用post方法的时候，可以通过--data "user=dq"  方式来传递参数
-X get  使用get方法，参数直接放到url后面
```

3、指定referer
```
--referer url
比如 curl --referer "www.baidu.com" https://www.baidu.com
```

4、指定客户端的设备信息
```
--user-agent "User Agent"
 比如curl -v --user-agent "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/63.0.3239.84 Safari/537.36" https://www.baidu.com
```

5、指定cookie
```
--cookie "name=xxx"
 比如curl -v --cookie "name=dqs” https://www.baidu.com
```

6、添加http认证
```
--user name:password
 比如curl -v --user dq:123456 http://baidu.com
```

7、指定host
```
-H "host:val"
 比如curl -H "host:www.findme.wang" 60.205.21.85:80
```

8、添加header头
```
-H "key:val"
 比如curl -v -H "Accept:text/html" https://www.baidu.com
```

9、设置代理
```
-x host:port
-x [protocol://[user:pwd@]host[:port]
--proxy [protocol://[user:pwd@]host[:port]
比如curl -x 192.168.13.149:8081 127.0.0.1
```


10、上传文件和图片
```
-F "filename=@fileName" 上传文件
-F "image=@fileName" 上传图片
比如curl -F "filename=@test.txt" -F "image=@img.png" http://127.0.0.1
```

### 二、看响应头
```
curl命令默认请求返回的是响应内容，如果想只看响应头，可以通过-I参数
curl -I  只看响应头
curl -i  看响应头+响应体
```

### 三、查看请求和响应所有内容
`curl -v  其中 -v 是--verbose的缩写`

### 四、解析host
可能有的时候，我们不想改下机器的hosts文件，可以使用curl的--resolve 选项来指定host的解析
```
curl --resolve HOST:PORT:ADDRESS
如：curl --resolve www.findme.wang:80:60.205.21.85 http://www.findme.wang
```

### 五、指定证书
```
curl -cacert
如：curl --cacert conf/test.pem  https://127.0.0.1:443
```

### 六、实例
1、参数值中带单引号的post请求，换行用“\”
```
curl --location --request POST 'http://localhost:8080/api/admin/movie/ups/search/label/content' \
--header 'Content-Type: application/json' \
--data-raw '{
    "taskId": 130,
    "taskName": "20岁以下人群用户id",
    "desc": "年龄=20岁以下",
    "expr": "age_range in ('\''0'\'')",
    "type": 0,
    "channel": "'\’'sdsdfa'\''",
    "search": "user_id",
    "num": 31749
}'
```

2、get请求
`curl -X GET --header 'Accept: application/json' 'http://localhost:8080/api/label/channel'`

### 参考
http://www.findme.wang/blog/detail/id/287.html
