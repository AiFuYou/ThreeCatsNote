要使用Shell代码给Slack上的某条消息添加reaction，您可以使用cURL命令通过Slack的API来完成。以下是一个示例代码，假设您已经拥有了Slack的访问令牌（`token`）和要添加reaction的相关信息（`channel_id`、`message_ts`和`reaction`）：

```bash
#!/bin/bash

token="YOUR_SLACK_TOKEN"
channel_id="YOUR_CHANNEL_ID"
message_ts="YOUR_MESSAGE_TIMESTAMP"
reaction="YOUR_REACTION_NAME"

curl -X POST -H "Authorization: Bearer $token" \
     -H "Content-Type: application/json" \
     -d '{"channel":"'"$channel_id"'","timestamp":"'"$message_ts"'","name":"'"$reaction"'"}' \
     "https://slack.com/api/reactions.add"
```

请将代码中的`YOUR_SLACK_TOKEN`、`YOUR_CHANNEL_ID`、`YOUR_MESSAGE_TIMESTAMP`和`YOUR_REACTION_NAME`替换为实际的值。

将上述代码保存为一个Shell脚本（例如`add_reaction.sh`），然后在终端中运行该脚本即可添加reaction。

请确保在运行脚本之前，您已经具有足够的权限来访问并操作Slack的API。
