---
title: "利用存留時間讓 DocumentDB 集合中的資料過期 | Microsoft Docs"
description: "利用 TTL，Microsoft Azure DocumentDB 提供了在一段時間後從系統自動清除文件的功能。"
services: documentdb
documentationcenter: 
keywords: "存留時間"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: documentdb
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/12/2016
ms.author: arramac
translationtype: Human Translation
ms.sourcegitcommit: 9f4105d1ab366994add0f75d634917ab9a063733
ms.openlocfilehash: 03486c23e4e939f1d84aa13af4308dc2059f9980


---
# <a name="expire-data-in-documentdb-collections-automatically-with-time-to-live"></a>利用存留時間讓 DocumentDB 集合中的資料自動過期
應用程式可以產生並儲存大量資料。 其中有些資料，例如電腦產生的事件資料、記錄檔和使用者工作階段資訊只能在有限的期間內使用。 一旦資料超過應用程式的需求，即可放心清除此資料並減少應用程式的儲存體需求。

利用「存留時間」或 TTL，Microsoft Azure DocumentDB 提供了在一段時間後從資料庫自動清除文件的功能。 預設存留時間可以在集合層級設定，並且在每份文件上覆寫。 一旦設定 TTL (做為集合預設值或在文件層級)，DocumentDB 就會自動移除自上次修改後存在一段時間 (以秒為單位) 的文件。

DocumentDB 中的存留時間會使用上次修改文件時的時間位移。 為了這麼做，它會使用每份文件上存在的 _ts 欄位。 _ts 欄位是 unix 樣式的 Epoch 時間戳記，表示日期和時間。 每次修改文件時就會更新 _ts 欄位。 

## <a name="ttl-behavior"></a>TTL 行為
TTL 功能是由兩個層級 (集合層級和文件層級) 的 TTL 屬性所控制。 屬性值會以秒設定，而且會被視為上次修改文件的 _ts 差異。

1. 集合的 DefaultTTL
   
   * 如果遺失 (或設為 null)，便不會自動刪除文件。
   * 如果存在且值為 "-1"= 無限 – 文件預設不會過期
   * 如果存在且值是某個數字 ("n") – 文件會在上次修改後的 "n"秒到期
2. 文件的 TTL︰ 
   
   * 僅在父集合有 DefaultTTL 時，才適用屬性。
   * 覆寫父集合的 DefaultTTL 值。

文件一過期 (ttl + _ts >= 目前的伺服器時間)，就會標示為「已過期」。 在此時間之後，不允許在這些文件上執行任何作業，而且將會從任何執行的查詢結果中排除。 這些文件會在系統中遭到實體刪除，而稍後在背景中伺機刪除。 這不會耗用集合預算中的任何 [要求單位 (RU)](documentdb-request-units.md) 。

上述邏輯可以顯示在下列矩陣中︰

|  | 集合上遺漏/未設定 DefaultTTL | 集合上的 DefaultTTL = -1 | 集合上的 DefaultTTL = "n" |
| --- |:--- |:--- |:--- |
| 集合上遺漏 TTL |文件層級沒有可覆寫的項目，因為文件和集合沒有 TTL 的概念。 |此集合中的所有文件都不會過期。 |此集合中的文件將會在間隔 n 過去時到期。 |
| 文件上的 TTL = -1 |文件層級沒有可覆寫的項目，因為集合未定義文件可以覆寫的 DefaultTTL 屬性。 系統無法解譯文件上的 TTL。 |此集合中的所有文件都不會過期。 |此集合中 TTL=-1 的文件永遠不會過期。 所有其他文件將在 "n" 間隔之後過期。 |
| 文件上的 TTL = n |文件層級沒有可覆寫的項目。 系統無法解譯文件上的 TTL。 |TTL = n 的文件將在間隔 n (以秒為單位) 之後到期。 其他文件會繼承間隔 -1 且永遠不會過期。 |TTL = n 的文件將在間隔 n (以秒為單位) 之後到期。 其他文件會繼承集合的間隔 "n"。 |

## <a name="configuring-ttl"></a>設定 TTL
根據預設，所有 DocumentDB 集合中和所有文件上的存留時間都會停用。

## <a name="enabling-ttl"></a>啟用 TTL
若要在集合上或集合內的文件上啟用 TTL，您需要將集合的 DefaultTTL 屬性設定為 -1 或非零的正數。 將 DefaultTTL 設定為 -1，表示集合中的所有文件都預設為永遠存留，但 DocumentDB 服務應監視此集合中已覆寫這個預設值的文件。

## <a name="configuring-default-ttl-on-a-collection"></a>在集合上設定預設 TTL
您可以在集合層級設定預設存留時間。 

若要在集合上設定 TTL，您必須提供非零的正數，指出集合中的所有文件在上次修改時間戳記 (_ts) 之後要到期的期間 (以秒為單位)。

或者，您可以將預設值設定為 -1，表示插入集合中的所有文件預設會無限期存留。

## <a name="setting-ttl-on-a-document"></a>在文件上設定 TTL
除了在集合上設定預設 TTL，您可以在文件層級設定特定的 TTL。 這麼做將會覆寫集合的預設值。

若要在文件上設定 TTL，您必須提供非零的正數，指出文件在上次修改時間戳記 (_ts) 之後要到期的期間 (以秒為單位)。

若要設定此到期位移，請在文件上設定 TTL 欄位。

如果文件沒有 TTL 欄位，則會套用集合的預設值。

如果已在集合層級停用 TTL，則會忽略文件上的 TTL 欄位，直到在集合上重新啟用 TTL 為止。

## <a name="extending-ttl-on-an-existing-document"></a>在現有文件上延長 TTL
您可以在文件上進行任何寫入作業，以重設文件上的 TTL。 這麼做會將 _ts 設定為目前的時間，並重新開始倒數文件到期的時間 (如 ttl 所設定)。

如果您想要變更文件的 ttl，您可以如同處理任何其他可設定的欄位一樣更新此欄位。

## <a name="removing-ttl-from-a-document"></a>從文件移除 TTL
如果文件上已設定 TTL，而您不再希望文件會到期，您可以擷取此文件、移除 TTL 欄位，然後取代伺服器上的文件。

移除文件的 TTL 欄位後，將會套用集合的預設值。

若要阻止文件到期且不要繼承集合的值，您必須將 TTL 值設定為 -1。

## <a name="disabling-ttl"></a>停用 TTL
若要在集合上完全停用 TTL 並阻止背景處理程序尋找過期的文件，則應刪除集合上的 DefaultTTL 屬性。

刪除此屬性與將它設定為 -1 不同。 設定為 -1，表示加入至集合的新文件會永遠存留，但是您可以在集合中的特定文件上覆寫此值。

從集合中完全移除此屬性，表示即使有已明確覆寫先前預設值的文件，所有文件也都不會過期。

## <a name="faq"></a>常見問題集
**TTL 的費用為何？**

在文件上設定 TTL 不會產生額外的費用。

**TTL 一旦到了，刪除我的文件要花多少時間？**

TTL 一旦到了，文件會立即到期，並將無法透過 CRUD 或查詢 API 存取。 

**文件上的 TTL 是否會對 RU 費用造成任何影響？**

否，在 DocumentDB 中透過 TTL 刪除過期的文件將不會影響 RU 費用。

**TTL 功能只會套用至整個文件，或者我可以讓個別的文件屬性值過期？**

TTL 會套用到整份文件。 如果您要讓文件的一部分過期，建議您從主要文件中將該部分擷取到個別的「已連結」文件，然後在該擷取文件上使用 TTL。

**TTL 功能是否有任何特定的編製索索引需求？**

是。 集合的[編製索引原則](documentdb-indexing-policies.md)必須設定為 [延遲] 或 [一致]。 嘗試在編製索引設為 [無] 的集合上設定 DefaultTTL 會造成錯誤，而嘗試在已設定 DefaultTTL 的集合上關閉索引編製也會造成錯誤。

## <a name="next-steps"></a>後續步驟
若要深入了解 Azure DocumentDB，請參閱服務的[*文件*](https://azure.microsoft.com/documentation/services/documentdb/)頁面。




<!--HONumber=Nov16_HO3-->


