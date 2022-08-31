
# 协议概述

```
Session
  |- session_id
  |- tags
  |- attributes
  |- events
       |- event_id
       |- tags 
       |- timestamp
       |- attributes
```

# 协议详述

```json
// 会话
"Session":
{
    "session_id": "",  // [Required] 会话ID
    "tags": "",        // [Optional] 标签（参考标签语义）
    "attributes": "",  // [Optional] 属性（参考会话语义）
    "events": [{}]     // [Required] 事件流 (定义:Event)
}
```

```json
// 事件
"Event":  {
    "event_id": "",                                          // [Required] 事件ID
    "tags": "",                                              // [Optional] 标签（参考标签语义） 
    "timestamp": "2022-08-31 15:29:01.209512872 +0000 UTC",  // [Required] 事件发生时间
    "attributes": "",                                        // [Optional] 属性（参考事件语义）
}
```
