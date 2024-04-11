要给Slack上的某条消息添加reaction，您可以使用Slack的API来完成。具体而言，您需要调用chat.postMessage方法中的reactions参数来添加reaction。

下面是使用Python来给消息添加reaction的示例代码：

```python
import requests

def add_reaction(token, channel_id, message_ts, reaction):
    url = f"https://slack.com/api/reactions.add"
    headers = {
        "Authorization": f"Bearer {token}",
        "Content-Type": "application/x-www-form-urlencoded"
    }
    data = {
        "channel": channel_id,
        "timestamp": message_ts,
        "name": reaction
    }
    response = requests.post(url, headers=headers, data=data)
    if response.ok:
        print("Reaction added successfully!")
    else:
        print("Failed to add reaction.")

# 设置您的Slack访问令牌
slack_token = "YOUR_SLACK_TOKEN"
# 设置要添加reaction的channel ID
channel_id = "YOUR_CHANNEL_ID"
# 设置要添加reaction的消息的时间戳
message_ts = "YOUR_MESSAGE_TIMESTAMP"
# 设置要添加的reaction的名称（比如 "thumbsup"）
reaction = "YOUR_REACTION_NAME"

# 添加reaction
add_reaction(slack_token, channel_id, message_ts, reaction)
```

请确保将代码中的"YOUR_SLACK_TOKEN"、"YOUR_CHANNEL_ID"、"YOUR_MESSAGE_TIMESTAMP"和"YOUR_REACTION_NAME"替换为实际的值。

这样，运行代码后就可以给指定的消息添加reaction了。请注意，您需要确保提供的Slack token有足够的权限来执行这个操作。
