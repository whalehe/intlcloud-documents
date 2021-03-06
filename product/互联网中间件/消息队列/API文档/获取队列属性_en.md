## 1. API Description

This API (GetQueueAttributes) is used to acquire the attributes of a created queue. Apart from the configurable attributes that were configured when creating the queue, the returned attributes will also include the creation time of the queue, the last modification time of the queue and the statistical information about the messages in the queue (approximate value).

Domain for public network API request:<font style="color:red">cmq-queue-region.api.qcloud.com</font>

Domain for private network API request:<font style="color:red">cmq-queue-region.api.tencentyun.com</font>

- region should be replaced by specific region: gz (Guangzhou), sh (Shanghai), bj (Beijing). The region value in the common parameter should be kept consistent with the one of the domain. In case of inconsistency, the domain region should prevail. The request should be sent to the region specified by the domain.
- Requests for accessing via public network domain support both HTTP and HTTPS. Requests for accessing via private network only support HTTP.
- Some of the input parameters are optional, so the default values are not required.
- All output parameters will be returned to the user when the request is successful; otherwise, at least code, message, and requestId will be returned.

## 2. Input Parameters

The following request parameter list only provides API request parameters. For other parameters, refer to [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| queueName | Yes | String | Queue name. This is unique under the same account in one region. The name of queue is a string with no more than 64 characters. It must start with letter, and the rest may contain letters, numbers and dashes (-). |


## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | 0: Succeed, 4440: Queue does not exist. For the meanings of other returned values, please refer to [Error Codes](/doc/api/431/5903). |
| message | String | Error message. |
| requestId | String | ID of the request generated by server. When there is an internal error on the server, users can submit this ID to backend to locate the problem. |
| maxMsgHeapNum | Int | Maximum number of messages in the queue. The available value range during beta test is `1,000,000 - 10,000,000`. It will be increased to `1,000,000-1,000,000,000` when officially launched. The default value is `10,000,000` during beta test, and `100,000,000` when officially launched. |
| pollingWaitSeconds | Int | Waiting time for messages to be received when using long-polling. Value range is 0-30 seconds. Default is 0. |
| visibilityTimeout | Int | Message visibility timeout. Value range is 1-43200 seconds (within 12 hours). Default is 30. |
| maxMsgSize | Int | Maximum message length. Value range is 1024-65536 Byte (1-64 K). Default is 65536. |
| msgRetentionSeconds | Int | How long the messages will be kept. Value range is 60-1296000 seconds (1 min-15 days). Default value is 345600 (4 days). |
| createTime | Int | Queue creation time. A Unix timestamp will be returned (accurate to second). |
| lastModifyTime | Int | The time when the queue attributes were modified for the last time. A Unix timestamp will be returned (accurate to second). |
| activeMsgNum | Int | Total number of messages in the queue whose status is Active (i.e. not Consumed). This is an approximate value. |
| inactiveMsgNum | Int | Total number of messages in the queue whose status is Inactive (i.e. being consumed). This is an approximate value. |
| rewindSeconds | Int | The maximum rewind time for messages in the queue. Value range is 0-43200 seconds. 0 means message rewind is disabled. |
| rewindmsgNum | Int | Number of messages that has been deleted by calling the DelMsg API but are still within the rewind time. |
| minMsgTime | Int | Minimum time for messages to be in the "not consumed" status (in seconds). |
| delayMsgNum | Int | Number of delayed messages. |
## 4. Example

Input:

<pre>
 https://domain/v2/index.php?Action=GetQueueAttributes
 &queueName=test-queue-123
 &<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common request parameters</a>>
</pre>

Output:

```
{
"code" : 0,
"message" : "",
"requestId":"14534664555",
"maxMsgHeapNum": 10000000,
"pollingWaitSeconds": 10,
"visibilityTimeout": 0,
"maxMsgSize": 65536,
"msgRetentionSeconds": 1296000,
"createTime":1462268960,
"lastModifyTime": 1462269960,
"activeMsgNum": 10000,
"inactiveMsgNum": 1000
}
```







