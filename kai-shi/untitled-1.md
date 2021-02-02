---
description: 预计阅读时间：4分钟
---

# 我们的应用程序

在本教程的其余部分中，我们将使用在Node.js中运行的简单待办事项列表管理器。如果您不熟悉Node.js，请不用担心！不需要真正的JavaScript经验！

此时，您的开发团队还很小，您只是在构建一个应用程序来证明您的MVP（最小可行产品）。您想展示它的工作原理和功能，而无需考虑它对大型团队，多个开发人员等的工作方式。

![](../.gitbook/assets/image%20%282%29.png)

### 开始我们的应用

在运行应用程序之前，我们需要将应用程序源代码下载到我们的计算机上。对于实际项目，通常将克隆存储库。但是，对于本教程，我们创建了一个包含应用程序的ZIP文件。

1. [下载应用程序内容](https://github.com/docker/getting-started/tree/master/app)。您可以拉整个项目，也可以将其下载为zip格式，然后提取应用文件夹以开始使用。
2. 下载后，使用您喜欢的代码编辑器打开项目。如果你对于编辑器选择困难，可以使用Visual Studio Code。您应该看到package.json和两个子目录（src和spec）。

![](../.gitbook/assets/image%20%284%29.png)

### 为应用程序创建镜像

为了构建应用程序，我们需要使用Dockerfile。 Dockerfile只是用于创建容器映像的基于文本的指令脚本。如果您以前创建过Dockerfile，则可能会在下面的Dockerfile中看到一些缺陷。但是，不用担心！我们将遍历它们。

1.在以下内容的package.json文件所在的文件夹中创建一个名为Dockerfile的文件。

```text
FROM node:12-alpine
 WORKDIR /app
 COPY . .
 RUN yarn install --production
 CMD ["node", "src/index.js"]
```

请检查文件Dockerfile是否没有文件扩展名，如.txt。一些编辑器可能会自动附加此文件扩展名，这将在下一步导致错误。

2.如果您尚未这样做，请打开一个终端，然后使用Dockerfile转到app目录。现在使用docker build命令构建容器镜像。

```text
 docker build -t getting-started .
```

此命令使用Dockerfile构建新的容器镜像。您可能已经注意到下载了许多“图层”（layers）。这是因为我们构建程序要从node:12-alpine镜像开始（以node:12-alpine为基础镜像）。但是由于我们机器上没有该镜像，因此需要下载该镜像。

下载镜像后，我们将其复制到应用程序中，并使用yarn安装了应用程序的依赖项。 CMD指令指定从该镜像启动容器时要运行的默认命令。

最后，`-t`标志标记我们的镜像。可以简单地将其视为最终镜像设置的易于理解的名称。由于我们将镜像命名为starting-starting，因此我们可以在运行容器时使用该镜像。

 docker build命令末尾的`.`告诉Docker应该在当前目录中查找Dockerfile。

### 启动应用程序容器

现在我们有了镜像，让我们运行该应用程序！我们将使用`docker run`命令（还记得以前的命令吗？）。

1.使用`docker run`命令启动您的容器，并指定我们刚刚创建的镜像名称：

```text
docker run -dp 3000:3000 getting-started
```

还记得`-d`和`-p`参数吗？我们正在“分离”模式下（在后台）运行新容器，并在主机的端口3000到容器的端口3000之间创建映射。如果没有端口映射，我们将无法访问该应用程序。

2.几秒钟后，打开Web浏览器到http://localhost:3000。您应该看到我们的应用程序！

![](../.gitbook/assets/image%20%285%29.png)

3.继续添加一个或两个项目，然后看它能按预期工作。您可以将项目标记为已完成并删除项目。您的前端已成功在后端存储项目！非常简单快捷，不是吗？

此时，您应该有一个正在运行的待办事项列表管理器，其中包含一些由您自己构建的项目！现在，让我们进行一些更改，并了解有关管理容器的信息。

如果快速浏览Docker Dashboard，您应该会看到两个容器正在运行（本教程和您刚启动的应用容器）！

![](../.gitbook/assets/image%20%286%29.png)

### 概括



