### 流程

```
连接 
登陆 
聊天: 私聊 , 入群/群聊 , 退群
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
   msg: string <=512 消息内容
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
    ERROR(0,"error")
    ,TIP(1,"tip") //一般消息
        , TIP_NEED_LOGIN(11,"tip_login") //提示登陆
        , TIP_NEED_INIT(11,"tip_init")   //提示初始化
        , TIP_OFFLINE(12,"tip_offline")   //提示离线
        , TIP_ONLINE(13,"tip_online")     //提示在线
        , TIP_INIT_OK(14,"tip_init_ok")  //初始化成功
    ,ACTION(2,"action")
        ,ACTION_INIT(21,"action-init")
        ,ACTION_QUIT(22,"action-quit")
        ,ACTION_GROUP_ADD(23,"action-add-group")
        ,ACTION_GROUP_QUIT(24,"action-quit-group")
    ,CHAT(3,"chat")
        ,CHAT_GIFT(31,"chat-gift") //礼物 暂不支持
        ,CHAT_FILE(32,"chat-file") //文件 暂不支持
    ,BOARDCAST(4,"boardcast")
 ```

关于登陆
- type : 2
- msg : sid
