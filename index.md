### 流程

```
连接 
登陆 
聊天: 私聊 , 入群/群聊 , 退群
断开
```

### 连接

根据**提供**的地址 端口连接聊天服务器

### 关于重连

客户端每10秒若未发送过数据,需要发送系统消息,内容为字符串"ping",否则服务器会关闭连接

### 消息协议
json字符串:
```
{
   type: int 0+ 类型
   msg: string <=512 消息内容[ping/{msgId}/{sid}/...]
   time: int 时间戳
   fromUid: int -1/1+ 发送者uid,-1为系统
   fromAvatar: string 发送者头像地址[客户端发送不需要]
   toUid: int 0+ 接受者uid,0为全部
   groupId: int 0+ 群组id[0-默认,1-聊天室1,2-聊天室2]
}
```

关于uid

toUid/fromUid|说明
-|-
-1|系统
0|全部
1+|单用户uid

关于type
```
    ERROR(0,"错误")
    ,TIP(1,"消息")
        , TIP_NEED_LOGIN(11,"消息-需要登陆")
        , TIP_NEED_INIT(11,"消息-需要初始化") //msg: sid
        , TIP_OFFLINE(12,"消息-离线")
        , TIP_ONLINE(13,"消息-在线")
        , TIP_INIT_OK(14,"消息-初始化成功")
        , TIP_PUSH_OK(15,"消息-推送成功") // msg: msgId
        , TIP_PUSH_FAIL(16,"消息-推送失败") // msg: msgId
    ,ACTION(2,"动作")
        ,ACTION_INIT(21,"动作-初始化")
        ,ACTION_QUIT(22,"动作-下线")
        ,ACTION_GROUP_ADD(23,"动作-入群")
        ,ACTION_GROUP_QUIT(24,"动作-出群")
    ,CHAT(3,"聊天") //消息内容
        ,CHAT_GIFT(31,"聊天-收到礼物") // msg: 礼物id
        ,CHAT_FILE(32,"聊天-收到文件") // msg: 文件地址
    ,BOARDCAST(4,"广播") //msg: 广播内容
 ```
