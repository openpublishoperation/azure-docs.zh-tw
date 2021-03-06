---
title: 了解最新的 Azure 客體 OS 版次 | Microsoft Docs
description: Azure 雲端服務客體作業系統的發行最新消息和 SDK 相容性。
services: cloud-services
documentationcenter: na
author: yuemlu
manager: timlt
editor: ''

ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/13/2016
ms.author: raiye

---
# Azure 客體 OS 版次與 SDK 相容性矩陣
提供適用於雲端服務的最新 Azure 客體作業系統版次的最新資訊。此資訊協助您在客體 OS停用之前規劃升級路徑。如果您設定角色來使用「自動化」客體 OS 更新，如 [Azure 客體 OS 更新設定][Azure 客體 OS 更新設定]所述，則不一定要閱讀此頁面。

> [!IMPORTANT]
> 此頁面適用於客體作業系統上執行的雲端服務 Web 角色和背景工作角色。不適用於 IaaS 虛擬機器。
> 
> 

<!-- -->

> [!TIP]
> 訂閱[客體作業系統更新 RSS 摘要][rss]，以接收所有客體作業系統變更的最及時性通知。
> 
> 

不確定客體 OS 為何或客體 OS 版次如何工作？ 請閱讀[本節內容](#how-it-works)。

## 新聞更新
###### **2016 年 9 月 13 日**
9 月客體 OS 的首度發行期間從 2016 年 9 月 13 日開始，預訂的正式發行日為 2016 日 10 月 13 日。

###### **2016 年 8 月 9 日**
8 月客體 OS 於 2016 年 8 月 9 日首度發行，並計畫於 2016 年 9 月 8 日發行。

###### **2016 年 7 月 13 日**
7 月的客體 OS 發行期間從 2016 年 7 月 13 日開始，預計於 2016 日 8 月 12 日正式發行。

###### **2016 年 6 月 15 日**
6 月的客體 OS 的首度發行期間從 2016 年 6 月 15 日開始，預訂的正式發行日為 2016 日 7 月 14 日。

###### **2016 年 5 月 17 日**
5 月的客體 OS 的首度發行期間從 2016 年 5 月 17 日開始，預訂的正式發行日為 2016 日 6 月 10 日。

###### **2016 年 4 月 18 日**
4 月的客體 OS 的度發行期間從 2016 年 4 月 18 日開始，預訂發行日為 2016 日 5 月 12 日。

###### **2016 年 3 月 14 日**
3 月的客體 OS 的首度發行期間從 2016 年 3 月 14 日開始，預訂發行日為 2016 日 4 月 8 日。

###### **2016 年 2 月 22 日**
2 月客體 OS 的首度發行期間從 2016 年 2 月 22 日開始，預訂發行日為 2016 年 3 月 9 日。

###### **2016 年 1 月 18 日**
1 月客體 OS 的首度發行期間從 2016 年 1 月 18 日開始，預訂發行日為 2016 年 2 月 12 日。

###### **2016 年 1 月 4 日**
11 月 201511-02 客體 OS 已在 2016 年 1 月 4 日發行以供部署。此作業系統版本並未設定為自動更新的預設作業系統，因此將客體 OS 部署至 11 月 201511-02 作業系統版本的佈建時間會略為拉長。

## 版次
## 系列 4 版次
**Windows Server 2012 R2**

支援 .NET 4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 具有 * 的日期可能會變更
> 
> 

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.36\_201609-01 |2016 年 10 月 13 日 |Post 4.38 |TBD |
| WA-GUEST-OS-4.35\_201608-01 |2016 年 9 月 13 日 |Post 4.37 |TBD |
| WA-GUEST-OS-4.34\_201607-01 |2016 年 8 月 8 日 |Post 4.36 |TBD |
| WA-GUEST-OS-4.33\_201606-01 |2016 年 7 月 13 日 |2016 年 10 月 13 日 |TBD |
| WA-GUEST-OS-4.32\_201605-01 |2016 年 6 月 10 日 |2016 年 9 月 8 日 |TBD |
| WA-GUEST-OS-4.31\_201604-01 |2016 年 5 月 2 日 |2016 年 8 月 13 日 |TBD |
| WA-GUEST-OS-4.30\_201603-01 |2016 年 4 月 7 日 |2016 年 7 月 10 日 |TBD |
| WA-GUEST-OS-4.29\_201602-02 |2016 年 3 月 12 日 |2016 年 6 月 2 日 |TBD |
| WA-GUEST-OS-4.28\_201601-01 |2016 年 2 月 12 日 |2016 年 5 月 7 日 |TBD |
| WA-GUEST-OS-4.27\_201512-01 |2016 年 1 月 12 日 |2016 年 4 月 12 日 |TBD |
| ~~WA-GUEST-OS-4.26\_201511-02~~ |2016 年 1 月 4 日 |2016 年 3 月 12 日 |TBD |
| ~~WA-GUEST-OS-4.26\_201511-01~~ |2015 年 12 月 10 日 |2016 年 3 月 12 日 |TBD |
| ~~WA-GUEST-OS-4.25\_201510-01~~ |2015 年 11 月 6 日 |2016 年 2 月 12 日 |TBD |
| ~~WA-GUEST-OS-4.24\_201509-01~~ |2015 年 10 月 1 日 |2016 年 1 月 10 日 |TBD |
| ~~WA-GUEST-OS-4.23\_201508-02~~ |2015 年 9 月 9 日 |2015 年 12 月 6 日 |TBD |
| ~~WA-GUEST-OS-4.22\_201507-02~~ |2015 年 8 月 7 日 |2015 年 11 月 1 日 |TBD |
| ~~WA-GUEST-OS-4.21\_201506-01~~ |2015 年 7 月 9 日 |2015 年 10 月 9 日 |TBD |
| ~~WA-GUEST-OS-4.20\_201505-02~~ |2015 年 6 月 12 日 |2015 年 9 月 7 日 |TBD |
| ~~WA-GUEST-OS-4.19\_201504-01~~ |2015 年 4 月 17 日 |2015 年 8 月 9 日 |TBD |

## 系列 3 版次
**Windows Server 2012**

支援 .NET 4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 具有 * 的日期可能會變更
> 
> 

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.43\_201609-01 |2016 年 10 月 13 日 |Post 3.45 |TBD |
| WA-GUEST-OS-3.42\_201608-01 |2016 年 9 月 13 日 |Post 3.44 |TBD |
| WA-GUEST-OS-3.41\_201607-01 |2016 年 8 月 8 日 |Post 3.43 |TBD |
| WA-GUEST-OS-3.40\_201606-01 |2016 年 7 月 13 日 |2016 年 10 月 13 日 |TBD |
| WA-GUEST-OS-3.39\_201605-01 |2016 年 6 月 10 日 |2016 年 9 月 8 日 |TBD |
| WA-GUEST-OS-3.38\_201604-01 |2016 年 5 月 2 日 |2016 年 8 月 13 日 |TBD |
| WA-GUEST-OS-3.37\_201603-01 |2016 年 4 月 7 日 |2016 年 7 月 10 日 |TBD |
| WA-GUEST-OS-3.36\_201602-02 |2016 年 3 月 12 日 |2016 年 6 月 2 日 |TBD |
| WA-GUEST-OS-3.35\_201601-01 |2016 年 2 月 12 日 |2016 年 5 月 7 日 |TBD |
| WA-GUEST-OS-3.34\_201512-01 |2016 年 1 月 12 日 |2016 年 4 月 12 日 |TBD |
| ~~WA-GUEST-OS-3.33\_201511-02~~ |2016 年 1 月 4 日 |2016 年 3 月 12 日 |TBD |
| ~~WA-GUEST-OS-3.33\_201511-01~~ |2015 年 12 月 10 日 |2016 年 3 月 12 日 |TBD |
| ~~WA-GUEST-OS-3.32\_201510-01~~ |2015 年 11 月 6 日 |2016 年 2 月 12 日 |TBD |
| ~~WA-GUEST-OS-3.31\_201509-01~~ |2015 年 10 月 1 日 |2016 年 1 月 10 日 |TBD |
| ~~WA-GUEST-OS-3.30\_201508-02~~ |2015 年 9 月 9 日 |2015 年 12 月 6 日 |TBD |
| ~~WA-GUEST-OS-3.29\_201507-02~~ |2015 年 8 月 7 日 |2015 年 11 月 1 日 |TBD |
| ~~WA-GUEST-OS-3.28\_201506-01~~ |2015 年 7 月 9 日 |2015 年 10 月 9 日 |TBD |
| ~~WA-GUEST-OS-3.27\_201505-02~~ |2015 年 6 月 12 日 |2015 年 9 月 7 日 |TBD |
| ~~WA-GUEST-OS-3.26\_201504-01~~ |2015 年 4 月 17 日 |2015 年 8 月 9 日 |TBD |

## 系列 2 版次
**Windows Server 2008 R2 SP1**

支援 .NET 3.5、4.0、4.5、4.5.1、4.5.2

> [!NOTE]
> 具有 * 的日期可能會變更
> 
> 

| 組態字串 | 發行日期 | 停用日期 | 到期日期 |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.55\_201609-01 |2016 年 10 月 13 日 |Post 2.57 |TBD |
| WA-GUEST-OS-2.54\_201608-01 |2016 年 9 月 13 日 |Post 2.56 |TBD |
| WA-GUEST-OS-2.53\_201607-01 |2016 年 8 月 8 日 |Post 2.55 |TBD |
| WA-GUEST-OS-2.52\_201606-01 |2016 年 7 月 13 日 |2016 年 10 月 13 日 |TBD |
| WA-GUEST-OS-2.51\_201605-01 |2016 年 6 月 10 日 |2016 年 9 月 8 日 |TBD |
| WA-GUEST-OS-2.50\_201604-01 |2016 年 5 月 2 日 |2016 年 8 月 13 日 |TBD |
| WA-GUEST-OS-2.49\_201603-01 |2016 年 4 月 7 日 |2016 年 7 月 10 日 |TBD |
| WA-GUEST-OS-2.48\_201602-02 |2016 年 3 月 12 日 |2016 年 6 月 2 日 |TBD |
| WA-GUEST-OS-2.47\_201601-01 |2016 年 2 月 12 日 |2016 年 5 月 7 日 |TBD |
| WA-GUEST-OS-2.46\_201512-01 |2016 年 1 月 12 日 |2016 年 4 月 12 日 |TBD |
| ~~WA-GUEST-OS-2.45\_201511-02~~ |2016 年 1 月 4 日 |2016 年 3 月 12 日 |TBD |
| ~~WA-GUEST-OS-2.45\_201511-01~~ |2015 年 12 月 10 日 |2016 年 3 月 12 日 |TBD |
| ~~WA-GUEST-OS-2.44\_201510-01~~ |2015 年 11 月 6 日 |2016 年 2 月 12 日 |TBD |
| ~~WA-GUEST-OS-2.43\_201509-01~~ |2015 年 10 月 1 日 |2016 年 1 月 10 日 |TBD |
| ~~WA-GUEST-OS-2.42\_201508-02~~ |2015 年 9 月 9 日 |2015 年 12 月 6 日 |TBD |
| ~~WA-GUEST-OS-2.41\_201507-02~~ |2015 年 8 月 7 日 |2015 年 11 月 1 日 |TBD |
| ~~WA-GUEST-OS-2.40\_201506-01~~ |2015 年 7 月 9 日 |2015 年 10 月 9 日 |TBD |
| ~~WA-GUEST-OS-2.39\_201505-02~~ |2015 年 6 月 12 日 |2015 年 9 月 7 日 |TBD |
| ~~WA-GUEST-OS-2.38\_201504-01~~ |2015 年 4 月 17 日 |2015 年 8 月 9 日 |TBD |

## MSRC 修補程式更新
[這裡][patches]提供每月客體作業系統版次隨附的修補程式清單。

## SDK 支援
雖然 [Azure SDK 的淘汰原則][retire policy sdk]表示只支援高於 2.2 的版本，特定客體 OS 系列仍允許您使用較早版本。您應該一律使用最新版本的支援 SDK。

| 客體作業系統系列 | 相容的 SDK 版本 |
| --- | --- |
| 4 |版本 2.1+ |
| 3 |版本 1.8+ |
| 2 |版本 1.3+ |
| 1 |版本 1.0+ |

## 客體作業系統版次資訊
有三個重要的客體 OS 版次日期︰**發行**日期、**停用**日期，以及**到期**日期。客體 OS 在入口網站時會視為可用，且可以選擇作為目標客體 OS。當客體 OS 到達**停用**日期，會從 Azure 中移除。不過，以該客體 OS 為目標的任何雲端服務將仍正常運作。

**停用**日期和**到期**日期之間的時間範圍，提供一個緩衝區，讓您可以輕鬆從一個客體 OS 轉換到到較新的客體 OS。如果您使用「自動化」作為客體 OS，則一律會是最新版本，不必擔心過期問題。

當**到期**日期已過，任何仍在使用該客體 OS 的雲端服務將會遭到停止、刪除或強制升級。您可以在[這裡][retirepolicy]閱讀更多有關淘汰原則的資訊。

## 客體 OS 系列版本說明
客體作業系統系列以 Microsoft Windows Server 的發行版本為基礎。客體作業系統是指執行 Azure 雲端服務的基礎作業系統。每一個客體作業系統都有系列、版本和版次號碼。

* **客體 OS 系列**是客體 OS 所根據的 Windows Server 作業系統版次。例如，「系列 3」以 Windows Server 2012 為基礎。
* **客體 OS 版本**是客體 OS 系列映像，加上新的客體 OS 版本發行當天可用的相關 [Microsoft Security Response Center (MSRC)][msrc] 修補程式。不一定包含所有修補程式。
  
    編號從 0 開始，每增加一組新的更新就加 1。必要時才會顯示尾端的零。亦即，2.10 版是與 2.1 版不同且更新的版本。
* **客體 OS 版次**是指客體 OS 版本的再發行版次。如果 Microsoft 在測試期間發現問題而需要變更時，就會推出再發行版次。最新的版次一律取代任何先前的版次，無論是否公開都一樣。Azure 傳統入口網站只允許使用者挑選特定版本的最新版次。視錯誤的嚴重性而定，通常不會強制升級舊版次上執行的部署。

在下列範例中，2 是系列，12 是版本，"rel2" 是版次。

**客體作業系統版次** - 2.12 rel2

**此版次的組態字串** - WA-GUEST-OS-2.12\_201208-02

客體作業系統的組態字串內嵌這項相同的資訊，還附上指出該版次考量哪些 MSRC 修補程式的日期。在此範例中，針對 Widows Server 2008 R2 推出的 MSRC 修補程式 (達到且包含 2012 年 8 月) 已考量納入。只會包含明確適用於該 Windows Server 版本的修補程式。例如，如果某個 MSRC 修補程式適用於 Microsoft Office，則不會納入，因為該產品不是 Windows Server 基本映像的一部分。

## 客體作業系統的系統更新程序
此頁面包含即將推出的客體作業系統版次的相關資訊。客戶表示想要知道何時推出版次，因為他們的雲端服務角色如果設為「自動」更新，將重新啟動。在每月第二個星期二發行 MSRC 更新後，通常至少 5 天才會推出客體作業系統版次。新版次包含每個客體作業系統系列的相關 MSRC 修補程式。

Microsoft Azure 正持續發行更新。客體作業系統只是這過程中的一項更新。影響版次的因素太多，無法在這裡完整列出。此外，Azure 實際上是在成千上萬個電腦上執行。這表示不可能指出您的角色重新啟動的確切日期和時間。我們會在[客體作業系統更新 RSS 摘要][rss]中隨時提供最新資訊，但請視為大約的時間。我們知道這對客戶造成困擾，所以正計劃對重新啟動設限或訂定時間。

新版次的客體作業系統發行時，需要一段時間才會完全傳播到整個 Azure。當服務更新到新的客體作業系統時，它們會重新啟動，讓更新網域生效。設為「自動」更新的服務會最先取得一個版次。更新之後，您在 Azure 傳統入口網站中會看到您的服務列出新的客體作業系統版本。此期間可能再度發行版次。某些版本的部署期間可能很長，而且在官方發行日期之後，可能經過許多個星期都還不會進行自動升級重新啟動。當客體作業系統推出時，您可以從入口網站或組態檔中明確地選擇該版本。

關於重新啟動的大量實用資訊，以及客體和主機作業系統更新的更多技術細節的線索，請參閱 MSDN 部落格文章＜[角色執行個體由於作業系統升級而重新啟動][restarts]＞。

如果您手動更新客體作業系統，請參閱[客體作業系統淘汰原則][retirepolicy]。

## 客體作業系統可支援性和淘汰原則
[這裡][retirepolicy]說明客體作業系統可支援性和淘汰原則。

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure 客體 OS 更新設定]: cloud-services-how-to-configure.md
[rss]: http://sxp.microsoft.com/feeds/3.0/msdntn/WindowsAzureOSUpdates
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md


<!---HONumber=AcomDC_0921_2016-->