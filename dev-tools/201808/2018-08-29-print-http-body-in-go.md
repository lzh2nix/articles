# 在Go中友好的打印http的request

开始我们使用的方式可能就是fmt.Println(req)了, 但是这种方式的打印看上去很不友好.你看到的request可能是这样的.

```shell
&{GET /hello/lizhengqian HTTP/1.1 1 1 map[User-Agent:[PostmanRuntime/7.1.1] Accept:[*/*] Accept-Encoding:[gzip, deflate] Connection:[keep-alive] Cache-Control:[no-cache] Postman-Token:[8ad0dcda-a703-4a09-a54f-1e62a156e35c]] {} <nil> 0 [] false 0.0.0.0:8082 map[] map[] <nil> map[] 127.0.0.1:51577 /hello/lizhengqian <nil> <nil> <nil> 0xc4201ba640}
```
这里如果你对request的每个字段不太熟悉的话这里打印出来的东西就只能大概的去猜了.

偶然的一次机会找的了下面这段代码之后再也不能释手了, 很完美的将每个头信息打印出来了.

```go
requestDump, err := httputil.DumpRequest(req, true)
if err != nil {
fmt.Println(err)
}
fmt.Println(string(requestDump))
```
完美的输出

```shell
GET /hello/lizhengqian HTTP/1.1
Host: 0.0.0.0:8082
Accept: */*
Accept-Encoding: gzip, deflate
Cache-Control: no-cache
Connection: keep-alive
Postman-Token: 548c6c27-2f6c-491d-9fc3-31417d8345dc
User-Agent: PostmanRuntime/7.1.1
```
