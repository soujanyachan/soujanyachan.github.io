There were two specific replicable instances of double persistent messages in the Bada Business bot:  x1621317583969 (prod).  
----------------------------------------------------------------------------- 1 ------------------------------------------------------------------------------------------------------------------------------------------------------  
One seen in ticket id 100753 on Aug 10, 4.49pm IST.  
As below, the messages were found only once in agents-service logs and were saved correctly.  

```{"log":"2021-08-10T11:19:09.415Z [info][f6df3fa411d50ecb][sendMessageNotificationToCollaborators][x1621317583969][100753][you]: XMPP model Send message user_1628496592899 to user_1628496592899 and message: \"{\\\"type\\\":\\\"collaborator\\\",\\\"data\\\":{\\\"message\\\":\\\"Hii\\\",\\\"_id\\\":\\\"611260ad4ff7ee07f0a7d6e1\\\"},\\\"agentId\\\":\\\"deepika.verma@badabusiness.com\\\",\\\"source\\\":\\\"yellowmessenger\\\",\\\"ticketId\\\":\\\"100753\\\",\\\"uid\\\":\\\"6927179262086219360220043816\\\",\\\"messageType\\\":\\\"AGENT\\\"}\"","f_s":"agents-service","f_pod":"agents-service-bbf8976b5-h4xvp","time":"2021-08-10T11:19:09+00:00"}
{"log":"2021-08-10T11:20:27.206Z [info][e4ba5cfdffa46428][sendMessageNotificationToCollaborators][x1621317583969][100753][you]: XMPP model Send message user_1628496592899 to user_1628496592899 and message: \"{\\\"type\\\":\\\"collaborator\\\",\\\"data\\\":{\\\"message\\\":\\\"How may I assist you today? \\\",\\\"_id\\\":\\\"611260fb35cde52fa6cf2b9d\\\"},\\\"agentId\\\":\\\"deepika.verma@badabusiness.com\\\",\\\"source\\\":\\\"yellowmessenger\\\",\\\"ticketId\\\":\\\"100753\\\",\\\"uid\\\":\\\"6927179262086219360220043816\\\",\\\"messageType\\\":\\\"AGENT\\\"}\"","f_s":"agents-service","f_pod":"agents-service-bbf8976b5-r29bb","time":"2021-08-10T11:20:27+00:00"}
```
But in controller the `/receive` route got this data, i.e. some agent messages were stored in the  `welcomeMessage` field:  

```{"message":"ym-debug 6927179262086219360220043816 {\"message\":\"Mere paas ek distribution hai,  but mujhe samajh nahin aa raha ki main kis rate mein apna product bechun\",\"source\":\"yellowmessenger\",\"subSource\":\"sdk\",\"messageId\":1628594479189,\"pageUrl\":\"file:///android_asset/index.html\",\"welcomeMessage\":{\"message\":[{\"message\":\"Hii\",\"_id\":\"611260ad4ff7ee07f0a7d6e1\"},{\"message\":\"How may I assist you today? \",\"_id\":\"611260fb35cde52fa6cf2b9d\"}],\"count\":3,\"latestCreated\":\"2021-08-10T11:19:04.935Z\"},\"sync\":\"\",\"isSensitiveInfo\":false} x1621317583969","level":"info","f_s":"controller","hostName":"controller-b89ddf447-st4rd","namespace":"services","timestamp":"2021-08-10T11:21:20.305Z","time":"2021-08-10T11:21:20+00:00"}
```
Unsure why were some agent messages were being stored in welcome messages but in controller code, we are saving welcome message data as bot messages. (`controller/models/executor.js`)  
```
 if (welcomeMessage) {
                                const welcomeMessageObject = {
                                    ...messageObject,
                                    _id: objectId(),
                                    messageType: 'BOT',
                                    messageAdditionalData: { count: welcomeMessage.count },
                                    message: JSON.stringify(welcomeMessage.message),
                                    created: welcomeMessage.latestCreated || new Date(),
                                    updated: welcomeMessage.latestCreated || new Date()
                                };
                                dataServicesInstance.post(`/internal/message/create/${mapping.userName}`, welcomeMessageObject);
```
This is why a single pair of messages got repeated once as AGENT messages and once as BOT messages.  
----------------------------------------------------------------------------- 2 ------------------------------------------------------------------------------------------------------------------------------------------------------  
Another instance was in ticket id 101224 on Aug 11 5.17 pm IST. The message was sent twice over xmpp to the assigned agent as below:  
```
{"log":"2021-08-11T11:47:03.940Z [info][3a0303fcbf65e62a][sendMessageNotificationToCollaborators][x1621317583969][101221][you]: XMPP model Send message user_1628496709325 to user_1628496709325 and message: \"{\\\"type\\\":\\\"collaborator\\\",\\\"data\\\":{\\\"message\\\":\\\"Mere pas ek relevant video hai, aap kab dekhna chahenge?\\\",\\\"_id\\\":\\\"6113b8b7910daec5f53333a0\\\"},\\\"agentId\\\":\\\"tanya.taneja@badabusiness.com\\\",\\\"source\\\":\\\"yellowmessenger\\\",\\\"ticketId\\\":\\\"101224\\\",\\\"uid\\\":\\\"16743544944131824725644208647\\\",\\\"messageType\\\":\\\"AGENT\\\"}\"","f_s":"agents-service","f_pod":"agents-service-57db4b5d88-24qvj","time":"2021-08-11T11:47:03+00:00"}
{"log":"2021-08-11T11:47:03.628Z [info][82df34b0c4a74065][sendMessageNotificationToCollaborators][x1621317583969][101221][you]: XMPP model Send message user_1628496709325 to user_1628496709325 and message: \"{\\\"type\\\":\\\"collaborator\\\",\\\"data\\\":{\\\"message\\\":\\\"Mere pas ek relevant video hai, aap kab dekhna chahenge?\\\",\\\"_id\\\":\\\"6113b8b701ec7a3f9ffe2bde\\\"},\\\"agentId\\\":\\\"tanya.taneja@badabusiness.com\\\",\\\"source\\\":\\\"yellowmessenger\\\",\\\"ticketId\\\":\\\"101224\\\",\\\"uid\\\":\\\"16743544944131824725644208647\\\",\\\"messageType\\\":\\\"AGENT\\\"}\"","f_s":"agents-service","f_pod":"agents-service-57db4b5d88-6f529","time":"2021-08-11T11:47:03+00:00"}
```
Following the trace id, we find that the message was also received twice by agent-service. (ticket id is wrong in the logs for some reason, the time is correct)  
```
{"log":"2021-08-11T11:47:03.796Z [info][3a0303fcbf65e62a][x1621317583969][101221][you]: Sending Agent message...","f_s":"agents-service","f_pod":"agents-service-57db4b5d88-24qvj","time":"2021-08-11T11:47:03+00:00"}
{"log":"2021-08-11T11:47:03.545Z [info][82df34b0c4a74065][x1621317583969][101221][you]: Sending Agent message...","f_s":"agents-service","f_pod":"agents-service-57db4b5d88-6f529","time":"2021-08-11T11:47:03+00:00"}
```