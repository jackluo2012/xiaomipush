# xiaomipush
小米推送服务 Golang SDK
fork 的 github.com/yilee/xiaomi-push 这个,本来想直接提的,发现没有权限,
主要是加入了正式和测试地址,公司集成ios和android的,ios没有测试环境
只能在sndbox里面测试
Production ready, full golang implementation of Xiaomi Push API (http://dev.xiaomi.com/console/?page=appservice&mod=push)

```Go
//andoird                          AppSecret            Bundle ID              正试环境              
var Aclient = xiaomipush.NewClient("yourappSecret", []string{"packageName"},xiaomipush.ProductionHost)
//ios                              AppSecret            Bundle ID              ios测试环境
var Iclient = xiaomipush.NewClient("yourappSecret", []string{"packageName"},xiaomipush.DevelopHost)

func main() {
    //封装信息
    	var msg *xiaomipush.Message = xiaomipush.NewAndroidMessage("娱乐热点", title)
    	//添加扩长字段
    	msg.AddExtra("cmstype","hot")
    	msg.AddExtra("url",url)
    	msg.AddExtra("title",title)
    	//推送ios
    	iosresult,iosErr := Iclient.BroadcastAll(context.Background(), msg)
    	anroidresult,androidErr := Aclient.BroadcastAll(context.Background(), msg)
    
    	if iosErr != nil {
    		fmt.Println( "ios 推送失败")
    	}
    	if androidErr != nil {
    		fmt.Println( "Android 推送失败")
    	}
    	if iosresult.Result.Result == "ok" && anroidresult.Result.Result == "ok" {
    		fmt.Println( "推送成功")    		
    	}
    	fmt.Println( "推送失败")
   	
}

```

### Sender APIs

- [x] Send(msg *Message, regID string)
- [x] SendToList(msg *Message, regIDList []string)
- [x] SendTargetMessageList(msgList []*TargetedMessage)
- [x] SendToAlias(msg *Message, alias string)
- [x] SendToAliasList(msg *Message, aliasList []string)
- [x] SendToUserAccount(msg *Message, userAccount string) 
- [x] SendToUserAccountList(msg *Message, accountList []string)
- [x] Broadcast(msg *Message, topic string)
- [x] BroadcastAll(msg *Message) (*SendResult, error)
- [x] MultiTopicBroadcast(msg *Message, topics []string, topicOP TopicOP)
- [x] CheckScheduleJobExist(msgID string)
- [x] DeleteScheduleJob(msgID string) (*Result, error)
- [x] DeleteScheduleJobByJobKey(jobKey string) (*Result, error) 

### Stats APIs

- [x] Stats(start, end, packageName string)
- [x] GetMessageStatusByMsgID(msgID string) (*SingleStatusResult, error)
- [x] GetMessageStatusByJobKey(jobKey string) (*BatchStatusResult, error) 
- [x] GetMessageStatusPeriod(beginTime, endTime int64) (*BatchStatusResult, error) 

### Subscription APIs

- [x] SubscribeTopicForRegID(regID, topic, category string) (*Result, error)
- [x] SubscribeTopicForRegIDList(regIDList []string, topic, category string) (*Result, error)
- [x] UnSubscribeTopicForRegID(regID, topic, category string) (*Result, error)
- [x] UnSubscribeTopicForRegIDList(regIDList []string, topic, category string) (*Result, error)
- [x] SubscribeTopicByAlias(aliases []string, topic, category string) (*Result, error)
- [x] UnSubscribeTopicByAlias(aliases []string, topic, category string) (*Result, error)

### Feedback APIs

- [x] GetInvalidRegIDs() (*InvalidRegIDsResult, error)

### DevTools APIs

- [x] GetAliasesOfRegID(regID string) (*AliasesOfRegIDResult, error)
- [x] GetTopicsOfRegID(regID string) (*TopicsOfRegIDResult, error)
