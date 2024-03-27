在Jenkins中使用botUser模式给Slack发送长消息并且要实现折叠，可以通过发送一个带有"attachments"的消息来实现。Slack的附件可以包含大量的文本，并且可以通过用户的交互来折叠和展开。

分成以下步骤：

1. 首先，确保你的Jenkins集成了Slack，并且botUser模式已经激活。

2. 使用Jenkins pipeline中的`slackSend`函数，构建一个有`attachments`的消息。

一个基本的例子是：

```groovy
slackSend(color: 'good', message: '简要消息（Brief message）', attachments: [
    [
        fallback: '详细文本（Detailed text）',
        text: "这里是长内容，会自动显示折叠按钮。\n${longTextVariable}",
        color: '#36a64f', // 绿色
        mrkdwn_in: ["text"]
    ]
])
```

在这个例子中，`longTextVariable` 是一个变量，您应该在之前定义它，并在其中存储您要发送的长文本内容。这个附件会在Slack中展示为一个可以展开/折叠的部分。

注意，上述代码块应该在一个Jenkins pipeline脚本中执行，并且你需要将 `longTextVariable` 替换为实际的长文本。

3. 如果你正在使用一个自由风格的Jenkins job，你可能需要使用其他方式或插件来发送带有attachments的Slack消息。

常见的做法是，在Jenkins中构建自动化任务时用script步骤来发送curl命令，通过Slack API 发送复杂的消息。这需要生成一个具有合适权限的Slack token，并在API调用中使用该token。

```shell
curl -X POST -H 'Authorization: Bearer xoxb-your-token' -H 'Content-type: application/json' --data '{
    "channel": "YOUR_CHANNEL_ID",
    "text": "简要消息（Brief message）",
    "attachments": [
        {
            "fallback": "详细文本（Detailed text）",
            "text": "这里是长内容，会自动显示折叠按钮。",
            "color": "#36a64f",
            "mrkdwn_in": ["text"]
        }
    ]
}' https://slack.com/api/chat.postMessage
```

请记住确保将`xoxb-your-token`替换为你的实际Slack Bot User OAuth Access Token，以及`YOUR_CHANNEL_ID`替换为你想要发送消息的Slack频道ID。上述Curl命令可以在Jenkins job中作为shell步骤执行。

Slack中的折叠通常是在视觉上进行的，针对附件以更紧凑的形式展示，不会完全隐藏消息的主体内容。然而，如果用户感觉文本太长，他们可以选择不展开附件或者仅仅浏览简要部分。
