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



