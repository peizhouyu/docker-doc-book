---
description: 预计阅读时间：3分钟
---

# 更新我们的应用程序

作为一项小需求，产品团队已要求我们在没有待办事项列表项时更改“空白文本”。他们想将其转换为以下内容：

{% hint style="info" %}
You have no todo items yet! Add one above!
{% endhint %}

很简单，对吧？让我们进行更改。

### 更新我们的源代码

1.在`src/static/js/app.js`文件中，更新第56行以使用新的空文本。

```text
- <p className="text-center">No items yet! Add one above!</p>
+ <p className="text-center">You have no todo items yet! Add one above!</p>
```

2.让我们使用之前使用的相同命令构建一个新版本的镜像。

```text
docker build -t getting-started . 
```

3.让我们使用更新后的代码启动一个新容器。

```text
docker run -dp 3000:3000 getting-started 
```

哦！您可能会看到这样的错误（ID将有所不同）：

```text
docker: Error response from daemon: driver failed programming external connectivity on endpoint laughing_burnell 
(bb242b2ca4d67eba76e79474fb36bb5125708ebdabd7f45c8eaf16caaabde9dd): Bind for 0.0.0.0:3000 failed: port is already allocated.
```

所以发生了什么事？我们无法启动新容器，因为旧容器仍在运行。之所以出现此问题，是因为该容器正在使用主机的端口3000，并且计算机上只有一个进程（包括容器）可以侦听特定的端口。要解决此问题，我们需要删除旧的容器。

### 更新我们的旧容器

要移除容器，首先需要将其停止。一旦停止，就可以将其删除。我们有两种方法可以删除旧容器。随意选择最适合自己的方式。

#### 使用CLI删除容器

1.使用`docker ps`命令获取容器的ID。

```text
docker ps
```

2.使用`docker stop`命令停止容器。

```text
# Swap out <the-container-id> with the ID from docker ps
 docker stop <the-container-id>
```

3.容器停止后，您可以使用`docker rm`命令将其删除。

```text
docker rm <the-container-id>
```

{% hint style="info" %}
提示：

您可以通过在docker rm命令中添加“ force”参数来在单个命令中停止和删除容器。例如：

`docker rm -f <the-container-id>`
{% endhint %}

#### 使用Docker Dashboard移除容器

如果打开Docker仪表板，则可以单击两次删除容器！肯定比查找容器ID并将其删除要容易得多。

1.在仪表板打开的情况下，将鼠标悬停在应用程序容器上方，您会看到一系列操作按钮出现在右侧。

2.单击垃圾桶图标以删除容器。

3.确认删除操作，您就可以完成！

![](../.gitbook/assets/image%20%2810%29.png)

#### 启动我们更新的应用程序容器

1.现在，启动更新的应用程序。

```text
docker run -dp 3000:3000 getting-started
```

2.在`http://localhost:3000`上刷新浏览器，您应该会看到更新后的帮助文本！

![](../.gitbook/assets/image%20%286%29.png)

### 概括

尽管我们能够构建更新，但您可能已经注意到两件事：

* 我们待办事项列表中的所有现有项目都消失了！那不是一个很好的应用！我们将在短期内讨论。
* 如此小的更改涉及很多步骤。在接下来的部分中，我们将讨论如何在每次进行更改时如何查看代码更新而无需重建和启动新容器。

在讨论持久性之前，我们将快速了解如何与他人共享这些镜像。

