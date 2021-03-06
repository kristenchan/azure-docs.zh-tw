---
title: "快速入門：資料表 API 與 .NET - Azure Cosmos DB | Microsoft Docs"
description: "本快速入門示範如何使用 Azure Cosmos DB 資料表 API，以使用 Azure 入口網站與 .NET 建立應用程式"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quickstart connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 11/15/2017
ms.author: arramac
ms.openlocfilehash: 02317d1b74d10d0fb3a2a08d8f4292a6be0438c2
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2017
---
# <a name="quickstart-build-a-table-api-app-with-net-and-azure-cosmos-db"></a>快速入門：使用 .NET 與 Azure Cosmos DB 建置資料表 API 應用程式 

本快速入門示範如何使用 Java 與 Azure Cosmos DB [資料表 API](table-introduction.md)，以藉由從 GitHub 複製範例來建置應用程式。 本快速入門也會示範如何建立 Azure Cosmos DB 帳戶，以及如何使用資料總管在以 Web 為基礎的 Azure 入口網站中建立資料表和實體。

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立及查詢文件、索引鍵/值及圖形資料庫，所有這些都受惠於位於 Azure Cosmos DB 核心的全域散發和水平調整功能。 

## <a name="prerequisites"></a>必要條件

如果尚未安裝 Visual Studio 2017，您可以下載並使用**免費的** [Visual Studio 2017 Community 版本](https://www.visualstudio.com/downloads/)。 務必在 Visual Studio 設定期間啟用 **Azure 開發**。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>新增資料表

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>新增範例資料

您現在可以使用資料總管將資料新增至您的新資料表。

1. 在資料總管中，展開 **sample-table**，按一下 [實體]，然後按一下 [新增實體]。

   ![在 Azure 入口網站的 [資料總管] 中建立新實體](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. 現在，將資料新增至 PartitionKey 值方塊和 RowKey 值方塊，然後按一下 [新增實體]。

   ![為新的實體設定磁碟分割索引鍵和資料列索引鍵](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    您現在可以在資料表中新增更多實體、編輯實體，或在資料總管中查詢資料。 資料總管也可供您調整輸送量，以及對資料表新增預存程序、使用者定義函式和觸發程序。

## <a name="clone-the-sample-application"></a>複製範例應用程式

現在，我們將從 Github 複製「資料表」應用程式、設定連接字串，然後執行它。 您會看到，以程式設計方式來處理資料有多麼的容易。 

1. 開啟 git 終端機視窗 (例如 git bash)，並使用 `cd` 命令變更至要安裝範例應用程式的資料夾。 

    ```bash
    cd "C:\git-samples"
    ```

2. 執行下列命令來複製範例存放庫。 此命令會在您的電腦上建立範例應用程式副本。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. 然後在 Visual Studio 中開啟 TableStorage 方案檔案。 

## <a name="update-your-connection-string"></a>更新您的連接字串

現在，返回 Azure 入口網站以取得連接字串資訊，並將它複製到應用程式中。 這可讓您的應用程式與託管資料庫進行通訊。 

1. 在 [Azure 入口網站](http://portal.azure.com/)中按一下 [連接字串]。 

    使用畫面右方的複製按鈕來複製連接字串。

    ![在 [連接字串] 窗格中檢視及複製「連接字串」](./media/create-table-dotnet/connection-string.png)

2. 在 Visual Studio 中，開啟 App.config 檔案。 

3. 將連接字串值貼到 App.config 檔案來做為 AzureCosmosDBTableAPIConnectionString 的值。 

    `<add key="CosmosDBStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://account-name.table.cosmosdb.net" />`    

    > [!NOTE]
    > 若要將此應用程式與「Azure 資料表」儲存體搭配使用，您必須變更 `App.config file` 中的連接字串。 使用帳戶名稱作為資料表帳戶名稱，使用金鑰作為「Azure 儲存體」主要金鑰。 <br>
    >`<add key="StandardStorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
    > 
    >

4. 儲存 App.config 檔案。

您現已更新應用程式，使其具有與 Azure Cosmos DB 通訊所需的所有資訊。 

## <a name="build-and-deploy-the-app"></a>建置並部署應用程式

1. 在 Visual Studio 中，於 [方案總管] 中的 **TableStorage** 專案上按一下滑鼠右鍵，然後按一下 [管理 NuGet 套件]。 

2. 在 NuGet [瀏覽] 方塊中，輸入「Microsoft.Azure.CosmosDB.Table」。

3. 從結果中，安裝 **Microsoft.Azure.CosmosDB.Table** 程式庫。 這會安裝 Azure Cosmos DB 資料表 API 套件以及所有相依性。

4. 按 CTRL + F5 來執行應用程式。

    主控台視窗會顯示要新增至 Azure Cosmos DB 中的新資料表資料庫的資料表資料。

    您現在可以返回 [資料總管]，以查看、查詢、修改及使用這項新資料。

## <a name="review-slas-in-the-azure-portal"></a>在 Azure 入口網站中檢閱 SLA

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a>後續步驟

在本快速入門中，您已了解如何建立 Azure Cosmos DB 帳戶、如何使用資料總管來建立資料表，以及如何執行應用程式。  現在，您可以使用資料表 API 來查詢您的資料。  

> [!div class="nextstepaction"]
> [將資料表資料匯入至資料表 API](table-import.md)

