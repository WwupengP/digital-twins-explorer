---
页面类型: sample
语言:
- javascript
- typescript
产品:
- azure-digital-twins
名称: Azure Digital Twins explorer
描述: A code sample for visualizing and managing an Azure Digital Twins instance
url资源标识: digital-twins-explorer
---

# Azure Digital Twins Explorer

**Azure Digital Twins Explorer** 是 [Azure Digital Twins service](https：//docs.microsoft.com/azure/digital-twins/overview) 服务的开发者工具。它允许您连接到 Azure 数字孪生实例来理解、可视化和修改您的数字孪生数据。

<img src="https：//raw.githubusercontent.com/Azure-Samples/digital-twins-explorer/main/media/digital-twins-explorer.png" alt="Image of digital-twins-explorer"/>

Azure Digital Twins Explorer 是一个单页 JavaScript 应用。
这个存储库包含Azure数字孪生资源管理器托管版本的代码，可以通过 [Azure portal](https：//portal.azure.com) 和 [explorer.digitaltwins.azure.net](https：//explorer.digitaltwins.azure.net) 访问该版本。也可以将应用程序作为 node.js 应用程序在本地运行.

此 README 包含特定于本地托管此代码库的信息和指导，包括：
* [本地运行示例的说明](#run-azure-digital-twins-explorer-locally)
* [将示例作为Docker应用程序运行的说明](#run-azure-digital-twins-explorer-with-docker)
* [首次运行实例的登录信息](#sign-in-on-first-run)
* [实验特性](#experimental-features)
* [扩展点](#extensibility-points)
* [服务](#services)

有关 Azure Digital Twins Explorer 托管版本和本地代码库特性的一般文档，请参阅[Azure Digital Twins 文档](https：//docs.microsoft.com/azure/digital-twins/overview)： 
* [Azure Digital Twins Explorer（预览版）](https：//docs.microsoft.com/azure/digital-twins/concepts-azure-digital-twins-explorer)
* [使用 Azure Digital Twins Explorer（预览版）](https：//docs.microsoft.com/azure/digital-twins/how-to-use-azure-digital-twins-explorer)



Azure 数字孪生 Explorer 是在MIT许可下授权的。请参阅微软 [开源代码准则](https：//opensource.microsoft.com/codeofconduct)

## 环境需求

Node.js 10+

## 本地运行 Azure Digital Twins Explorer

1. 设置一个 Azure Digital Twins 服务实例并赋予自己权限 (e.g. *Azure Digital Twins 所有者*)。有关说明，请参阅下面的操作文章：
    * [设置 Azure 数字孪生实例和身份验证](https：//docs.microsoft.com/azure/digital-twins/how-to-set-up-instance-portal)
1. 在本地运行时，Azure Digital Twins Explorer 将使用 Azure 默认凭证。为了进行身份验证，您可以在任何命令提示符中运行 **az login**。当您稍后运行 Azure Digital Twins Explorer 时，它将获取凭证。或者，您可以在 Visual Studio Code 中登录
1. 选择 **Download ZIP** 按钮将此示例代码的. ZIP文件下载到您的计算机上。解压 **digital-twins-explorer-<branch>.zip** 文件夹，或者，您可以克隆存储库。
1. 从 'client/src' 文件夹的命令提示符中运行 `npm install`，这将检索所有依赖项
    >**重要!** 由于依赖于 `npm-force-resolutions` 包来缓解底层安全问题，您将无法在任何包含空格的路径下安装。欲了解更多信息，请参阅此 [GitHub issue](https：//github.com/rogeriochaves/npm-force-resolutions/issues/17).
1. 在相同的命令提示符下，运行 `npm run start`。
    > 默认情况下，应用程序在端口3000上运行。如果要自定义端口，请修改 run 命令。例如，使用8080端口：
    >  * Linux/Mac (Bash)： `PORT=8080 npm run start`
    >  * Windows (cmd)： `set PORT=8080 && npm run start`
    > 注意：你的 Azure Digital Twins 应用注册必须有一个使用你正在使用的端口的回复URL - 例如：localhost：7000，如果这是你正在使用的端口。
1. 你的浏览器应该打开，应用程序应该出现.

关于如何使用docker运行数字孪生资源管理器，请参见下面的说明。

## 用Docker运行 Azure 数字孪生浏览器

1. 从根文件夹的命令提示符中，运行 `docker build -t azure-digital-twins-explorer`。这将为 Azure 数字孪生浏览器构建 Docker 映像。
1. 在相同的命令行提示符下，运行 `docker run -it -p3000：3000 azure-digital-twins-explorer`。
    > 默认情况下，应用程序在端口3000上运行。如果要自定义端口，请修改 run 命令。例如，使用 8080 端口运行 `docker run -it -p8080：3000 azure-digital-twins-explorer`.
    > 控制台将出现一条消息，要求您使用微软设备登录页面中的代码与您的web浏览器登录；之后，Azure 数字孪生浏览器应该启动。
    >  * 注意：当成功运行时，应用程序将显示一条消息，显示你必须打开的URL和端口来浏览应用程序。当在Docker中运行应用程序时，该信息可能不准确，因为其他端口可能已经暴露。请确保使用您之前选择的端口。
1. 现在，您可以打开web浏览器，浏览到 `http：//localhost：3000`(如果更改了端口，请将“3000”更改为适当的端口)。

## 在第一次运行时签到

初始身份验证由以下操作之一触发：
1. 点击右上角的Azure Digital Twins URL按钮
 
    <img src="https：//raw.githubusercontent.com/Azure-Samples/digital-twins-explorer/main/media/digital-twins-explorer-url.png" alt="sign-in icon" width="250"/>
1. 单击需要调用服务的操作。当您单击第一个命令时，Azure Digital Twins Explorer将打开一个对话框，提示您输入到服务实例的连接信息。

为了继续，你需要提供你想要访问的Azure Digital Twins实例的URL，以实例的**主机名**的形式加上前缀`https：//`。您可以在Azure Digital Twins实例的[Azure门户](https：//portal.azure.com)概览页面中找到实例的主机名。

<img src="https：//raw.githubusercontent.com/Azure-Samples/digital-twins-explorer/main/media/sign-in-dialog.png" alt="sign-in dialog" width="250"/>

要更改实例URL以连接到Azure Digital Twins的另一个实例，请单击右上角的登录按钮。
 
## 实验特性

除了本地操作，您还可以将Azure Digital Twins Explorer作为云应用程序运行。在云端，你可以使用Azure Digital Twins通过Azure SignalR服务发送的推送通知，实时更新你的数字孪生资源管理器。

### 在云端运行

1. 部署名为 `template.json` 的ARM模板，json文件位于Azure订阅的 `deployment` 文件夹下。
1. 使用 `npm run build` 来打包客户端应用程序。如果收到与内存相关的错误，可能需要设置' NODE_OPTIONS=——max_old_space_size=4096 '。
1. 从新的 `build` 文件，上传每个文件到ARM模板创建的新存储帐户中的 `web` 容器。
1. 使用 `dotnet publish -c Release -o ./publish` 打包函数应用程序。
1. 压缩的 `./publish` 文件夹中的内容，例如，在publish文件夹中，运行 `zip -r DigitalTwinsExplorerFunctions.zip * `。
1. 使用CLI发布函数应用： `az functionapp deployment source config-zip -g <resource_group> -n <app_name> --src <zip_file_path>`.
1. [可选] 对于与该工具一起使用的每个Azure Digital Twins环境 *where live telemetry through SignalR is required*, 部署 Azure 订阅中的模板 `template-eventgrid.json`。
1. 设置一个系统分配的身份，以允许函数代理访问Azure数字孪生服务。
    1. 在Azure中，从您的资源组中打开 ** Function App**资源。
    1. 在左侧版块中点击 **Identity**。
    1. 在 **System assigned** tab 下将 **Status** 状态改为开。
    1. 在你的资源组中, 选择 **Azure Digital Twins** 资源。
    1. 在左侧版块中点击 **Access Control (IAM)**。
    1. 点击 **+ Add**，然后点击 **Add role assignment**。
    1. 角色选择 **Azure Digital Twins Data Owner**。
    1. 分配 **System assigned managed identity - Functions App** 访问权限。
    1. 列表中选择 **Functions App** 。
    1. 点击 **Save**。

### 高级

当本地运行时，遥测流所需的事件网格和SignalR服务不可用。但是，如果您已经完成了云部署，则可以在本地利用这些服务来启用全部功能集。

这需要设置 `REACT_APP_BASE_ADT_URL` 环境变量来指向你的 Azure Functions 主机(例如，`https：//adtexplorer-<你的后缀>.azurewebsites.net`)。这可以在启动 `npm` 之前设置或通过在 `client` 文件夹下创建 `.env` 文件，并在文件中包含配置项 `REACT_APP_BASE_ADT_URL=https：//...`。

此外，需要将本地URL添加到Azure Function和SignalR服务的允许源中。在ARM模板中，默认的 `http：//localhost：3000` 路径是在部署过程中添加的;但是，如果站点运行在本地的不同端口上，那么这两个服务都需要通过Azure门户进行更新。
## 扩展特性

### 导入

从 `src/services/plugins` 目录中导入插件。每个插件都应该定义为一个带有单个函数的类：

```ts
tryLoad(file： File)： Promise<ImportModel | boolean>
```

如果插件可以导入文件，它应该返回一个 `ImportModel`。如果它不能导入该文件，它应该返回 `false`，以便导入服务可以与其他插件共享该文件。
`ImportModel` 的结构应该如下所示：

```ts
class DataModel {
  digitalTwinsFileInfo： DataFileInfoModel;
  digitalTwinsGraph： DataGraphModel;
  digitalTwinsModels： DigitalTwinModel[];
}

class DataFileInfoModel {
  fileVersion： string; // should be "1.0.0"
}

class DataGraphModel {
  digitalTwins： DigitalTwin[]; // objects align with structure returned by API
  relationships： DigitalTwinRelationship[]; // objects align with structure returned by API
}
```

新插件需要注册在 `src/services/ImportService.js` 文件顶部的 `ImportPlugins` 集合中。

目前提供了Excel和JSON的导入插件。要支持这两种插件的自定义格式，新插件需要首先放在 `ImportPlugins` 集合中，否则需要扩展插件来检测自定义格式(要么就地解析，要么返回 `false` 以允许另一个插件进行解析)。

`ExcelImportPlugin` 旨在支持额外的基于excel的格式。目前，所有文件都是通过 `standdexcelimportformat` 类解析的;然而，检查单元格内容以检测特定结构并调用另一个导入类将相对简单。

### 导出

图可以导出为JSON文件(然后可以重新导入)。文件的结构遵循上一节中描述的 `DataModel` 类。
导出由 `src/services/ExportService.js` 文件中的 `ExportService` 类管理。

要更改导出格式结构，可以重用 `ExportService` 中提取图表内容的现有逻辑，然后根据需要重新格式化。

### 视图

所有面板都在 `src/App.js` 文件中定义。这些配置对象是由黄金布局组件的需求定义的。

对于应用程序中的临时面板(例如导入预览)，可以考虑两种方法：
1. 对于像输出和控制台这样的面板，新的面板可以添加到 `optionalComponentsConfig` 集合中。这允许面板的状态(即打开或关闭)通过应用程序状态来管理，无论它是通过选项卡上的“X”关闭，还是通过配置关闭(如在首选项对话框中可用)。
1. 对于像导入预览这样的面板，可以根据需要手动添加到布局中。这可以通过pub/sub机制(参见下面和' App.js '中的 `componentDidMount` 方法)干净地完成。

### 查看命令

如果视图中有命令，建议创建一个专用的命令栏组件(基于 `src/components/GraphViewerComponent/GraphViewerCommandBarComponent.js` 中的组件)。它们利用Office Fabric UI `CommandBar` 组件，通过道具公开功能回调或直接管理操作。

### 发布/订阅

黄金布局组件包括一个发布/订阅消息总线，用于组件之间的通信。这是Azure Digital Twins Explorer的关键部分，用于在组件之间传递消息。

所有事件——通过发布和订阅方法——都定义在 `src/services/EventService.js` 文件中。其他事件可以通过添加到该文件中来定义。

发布/订阅消息总线在应用程序加载时不能立即可用;然而，事件服务将在此期间缓冲任何发布或子请求，然后在它们可用时应用它们。
## 服务

### 本地

当本地运行时，所有对Azure Digital Twins服务的请求都通过托管客户端应用程序的同一本地web服务器代理。这是在 `client/src/setupProxy.js` 文件中配置的。

### 云端

当在云中运行时，Azure Functions托管了三个服务来支持前端应用：
1. 代理：它通过Azure Digital Twins服务代理请求(与本地运行时使用的代理方式大致相同)。
1. SignalR：这允许客户端检索凭据，以访问SignalR服务进行实时遥测更新。它还验证了将信息从Azure Digital Twins服务流到Azure Digital Twins Explorer应用程序所需的端点和路由是否到位。如果函数的托管服务标识配置正确(即对资源组具有写权限并可以管理Azure Digital Twins服务)，那么它可以自己创建这些服务。
1. EventGrid：它接收来自事件网格的消息，并使用SignalR将它们广播给任何侦听的客户机。消息通过Azure Digital Twins端点和路由从Azure Digital Twins发送到函数。

> 注意：如果你在其他地方托管了应用程序，而不是Azure Functions。然后，我们建议您将内容安全策略添加到您的环境中，正如在 `proxies.json` 中定义的那样。
