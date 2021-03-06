---
title: "檢視 Azure Data Lake Store 的診斷記錄 | Microsoft Docs"
description: "了解如何設定及存取 Azure Data Lake Store 的診斷記錄  "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/05/2016
ms.author: nitinme
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 276033907d454a54b2d9d5354f8e1dc48a7b01d4


---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>存取 Azure Data Lake Store 的診斷記錄
了解如何啟用 Data Lake Store 帳戶的診斷記錄，以及如何檢視針對帳戶收集的記錄。

組織可以啟用 Azure Data Lake Store 帳戶的診斷記錄，以便收集資料存取稽核記錄，取得如存取資料的使用者清單、資料存取頻率、儲存在帳戶內的資料量等資訊。

## <a name="prerequisites"></a>必要條件
* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 遵循 [使用 Azure 入口網站開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)的指示。

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>啟用 Data Lake Store 帳戶的診斷記錄
1. 登入新的 [Azure 入口網站](https://portal.azure.com)。
2. 開啟 Data Lake Store 帳戶，接著在 Data Lake Store 帳戶刀鋒視窗中依序按一下 [設定] 和 [診斷設定]。
3. 在 [診斷]  刀鋒視窗中，變更下列項目以設定診斷記錄。
   
    ![啟用診斷記錄](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")
   
   * 將 [狀態] 設定為 [開啟] 以啟用診斷記錄。
   * 您可以選擇兩種不同的資料儲存/處理方法。
     * 選取 [匯出到事件中樞]  選項可將記錄資料串流到 Azure 事件中樞。 如果您有即時分析內送記錄的下游處理管線，很可能會使用這個選項。 如果您選取此選項，必須提供要使用的 Azure 事件中樞詳細資料。
     * 選取 [匯出到儲存體帳戶]  選項可將記錄儲存到 Azure 儲存體帳戶。 如果您想要保存資料以供日後批次處理，可以使用此選項。 如果您選取此選項，必須提供用來儲存記錄的 Azure 儲存體帳戶。
   * 指定要取得稽核記錄、要求記錄或兩者。
   * 指定的資料的保留天數。
   * 按一下 [儲存] 。

一旦您啟用了診斷設定，即可在 [診斷記錄]  索引標籤中查看記錄。

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>檢視 Data Lake Store 帳戶的診斷記錄
檢視 Data Lake Store 帳戶的記錄資料有兩種方式。

* 從 Data Lake Store 帳戶設定檢視
* 從儲存資料的 Azure 儲存體帳戶

### <a name="using-the-data-lake-store-settings-view"></a>使用 Data Lake Store 設定檢視
1. 在 Data Lake Store 帳戶的 [設定] 刀鋒視窗中，按一下 [診斷記錄]。
   
    ![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs") 
2. 在 [診斷記錄] 刀鋒視窗中，您應該會看到依照 [稽核記錄] 和 [要求記錄] 分類的記錄。
   
   * 要求記錄能擷取所有以 Data Lake Store 帳戶提出的 API 要求。
   * 稽核記錄與要求記錄相似，不過能針對以 Data Lake Store 帳戶執行之作業提供更詳細的明細。 例如，要求記錄中的一個上傳 API 呼叫可能會致使稽核記錄出現多個「附加」作業。
3. 針對每個記錄項目按一下 [下載]  連結來下載記錄。

### <a name="from-the-azure-storage-account-that-contains-log-data"></a>從包含記錄資料的 Azure 儲存體帳戶
1. 開啟與與用於記錄的 Data Lake Store 關聯的Azure 儲存體帳戶刀鋒視窗，然後按一下 [Blob]。 [Blob 服務]  刀鋒視窗會列出兩個容器。
   
    ![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")
   
   * 容器 **insights-logs-audit** 包含稽核記錄檔。
   * 容器 **insights-logs-requests** 包含要求記錄檔。
2. 在這些容器中，紀錄會儲存在下列結構底下。
   
    ![檢視診斷記錄](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")
   
    例如，稽核記錄檔的完整路徑可能是 `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    同樣的，要求記錄檔的完整路徑可能是 `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-the-structure-of-the-log-data"></a>了解記錄資料的結構
稽核和要求記錄採用 JSON 格式。 在本節中，我們要探討要求和稽核記錄的 JSON 結構。

### <a name="request-logs"></a>要求記錄
以下是採用 JSON 格式之要求記錄中的範例項目。 每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列。

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>要求記錄的結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| 分析 |String |記錄的時間戳記 (UTC 時間) |
| resourceId |String |作業發生之資源的識別碼 |
| category |String |記錄類別。 例如， **要求**。 |
| operationName |String |記錄的作業名稱。 例如，getfilestatus。 |
| resultType |String |作業的狀態。例如，200。 |
| callerIpAddress |String |提出要求之用戶端的 IP 位址 |
| correlationId |String |用來將一組相關記錄項目分組在一起的記錄識別碼 |
| 身分識別 |Object |產生記錄的身分識別 |
| properties |JSON |如需詳細資料，請參閱下文 |

#### <a name="request-log-properties-schema"></a>要求記錄屬性結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| HttpMethod |String |作業使用的 HTTP 方法。 例如，GET。 |
| Path |String |執行作業的所在路徑 |
| RequestContentLength |int |HTTP 要求的內容長度 |
| ClientRequestId |String |可唯一識別要求的識別碼 |
| StartTime |String |伺服器接收到要求的時間 |
| EndTime |String |伺服器傳送回應的時間 |

### <a name="audit-logs"></a>稽核記錄檔
以下是採用 JSON 格式之稽核記錄中的範例項目。 每個 Blob 會一個名為 **記錄** 的根物件，其中包含記錄檔物件的陣列

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>稽核記錄的結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| 分析 |String |記錄的時間戳記 (UTC 時間) |
| resourceId |String |作業發生之資源的識別碼 |
| category |String |記錄類別。 例如， **稽核**。 |
| operationName |String |記錄的作業名稱。 例如，getfilestatus。 |
| resultType |String |作業的狀態。例如，200。 |
| correlationId |String |用來將一組相關記錄項目分組在一起的記錄識別碼 |
| 身分識別 |Object |產生記錄的身分識別 |
| properties |JSON |如需詳細資料，請參閱下文 |

#### <a name="audit-log-properties-schema"></a>稽核記錄屬性結構描述
| Name | 類型 | 說明 |
| --- | --- | --- |
| StreamName |String |執行作業的所在路徑 |

## <a name="samples-to-process-the-log-data"></a>處理記錄資料的範例
Azure Data Lake Store 會提供有關如何處理和分析記錄資料的範例。 您可以在 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)找到範例。 

## <a name="see-also"></a>另請參閱
* [Azure 資料湖儲存區概觀](data-lake-store-overview.md)
* [保護資料湖存放區中的資料](data-lake-store-secure-data.md)




<!--HONumber=Nov16_HO3-->


