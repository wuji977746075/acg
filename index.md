### 流程

```
连接 
登陆 
聊天: 私聊 , 入群/群聊 , 退群
```

### 连接

根据**提供**的地址 端口连接聊天服务器

### 消息协议
json字符串:
```
{
   type:
   msg:
   time:
   fromUid:
   fromAvatar: 发送者头像地址[客户端发送不需要]
   toUid:
   groupId: 群组id[0-默认,1-聊天室1,2-聊天室2]
}
```

### 登陆
- type : 2
- msg : sid
