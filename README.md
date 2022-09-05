
# Protocol

- [V 1.0.0.0](./OpenRUM/proto/v1/proto.md)

## 传输协议

```
HTTP/HTTPS
```

## Request Header 参数

| Key | 说明 |
| -- | -- |
| Package-ID | 包的唯一ID，用于请求排重。<br>同一包会话性能数据的多次重试上报，包ID应保持一致。 |

## Request URL 参数

| 字段 | 名称 | 描述 | 备注 |
| -- | -- | -- | -- |
| version | protocol version | 协议版本号 | String |
| app_id | app ID | 应用ID | Number |
| session_id | session ID | 会话ID | String |

示例：

```
https://sdkupload.bonree.com/upload?version=1.0.0.0&app_id=78721&session_id=fd80f42e-f973-420d-a127-37bb2438d15b
```

## Request Body 协议格式

```
Json
```

## Request 报文示例

```
POST /upload?version=1.0.0.0&app_id=78721&session_id=fd80f42e-f973-420d-a127-37bb2438d15b HTTP/1.1
Package-ID: 5740e0b2-007c-4624-b144-6b9bcd93b242
Content-Type: application/json; charset=utf-8
Host: sdkupload.bonree.com
Connection: close
User-Agent: Paw/3.1.10 (Macintosh; OS X/10.16.0) GCDHTTPRequest
Content-Length: 288
 
{"session_id":"fd80f42e-f973-420d-a127-37bb2438d15b","tags":"交易业务","attributes":{"user.id":"Tom123"},"soe":{}}
```

## Tips

1. **数据为*分片上传*（当产生一次事件即可上送数据无需组成完成会话上传），上传频次因需控制；**
2. **会话内事件数据发生时间与controller接收时间偏差7天，超过则会话数据无效；**
3. **重复Package-ID在controller判重3次后，http request失效；**

## Response Body 协议格式

```
Json
```

## Response Body 数据

```json
{
    "code": 0,       // [Required] 响应码
    "error_msg": ""  // [Optional] 错误信息
}
```

## Response Body code说明

| 响应码 | 说明 |
| -- | -- |
| 0 | 成功 |
| 1 | 请求读取异常 |
| 2 | 协议解析异常 |
| 3 | 服务器内部异常 |
| 4 | 缺少必要参数 |
| 5 | 授权过期 |
