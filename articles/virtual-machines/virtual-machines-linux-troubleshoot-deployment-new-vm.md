---
title: "針對 Linux VM 部署-RM 進行疑難排解 | Microsoft Docs"
description: "針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
translationtype: Human Translation
ms.sourcegitcommit: 63cf1a5476a205da2f804fb2f408f4d35860835f
ms.openlocfilehash: 3790c6108c151c30ca12feb4af19ad0fd4ae1f68


---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a>針對在 Azure 中建立新 Linux 虛擬機器的 Resource Manager 部署問題進行疑難排解
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a>收集稽核記錄檔
若要開始進行排解疑難，請收集稽核記錄，識別與問題相關的錯誤。 下列連結提供此程序該遵循的更多詳細資訊。

[使用 Azure 入口網站針對資源群組部署進行疑難排解](../resource-manager-troubleshoot-deployments-portal.md)

[使用 Resource Manager 來稽核作業](../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

**Y：** 如果作業系統是一般化的 Linux，且上傳和 (或) 擷取它時使用的是一般化設定，就不會有任何錯誤。 同樣地，如果作業系統是特殊化的 Linux，且上傳和 (或) 擷取它時使用的是特殊化設定，就不會有任何錯誤。

**上傳錯誤：**

**N<sup>1</sup>：**如果作業系統是一般化的 Linux，但是上傳它時是以特殊化形式上傳，就會發生佈建逾時錯誤，因為 VM 會卡在佈建階段。

**N<sup>2</sup>：**如果作業系統是特殊化的 Linux，但是上傳它時是以一般化形式上傳，就會發生佈建失敗錯誤，因為新 VM 是以原始的電腦名稱、使用者名稱和密碼執行。

**解決方案：**

若要解決這兩個錯誤，請使用與作業系統相同的設定 (一般化/特殊化) 來上傳原始 VHD (可從內部部署環境取得)。 若要以一般化形式上傳，請務必先執行 -deprovision。

**擷取錯誤：**

**N<sup>3</sup>：**如果作業系統是一般化的 Linux，但是擷取它時是以特殊化形式擷取，就會發生佈建逾時錯誤，因為原始 VM 會因被標示為一般化而無法供使用。

**N<sup>4</sup>：**如果作業系統是特殊化的 Linux，但是擷取它時是以一般化形式擷取，就會發生佈建失敗錯誤，因為新 VM 是以原始的電腦名稱、使用者名稱和密碼執行。 此外，原始 VM 會因被標示為特殊化而無法供使用。

**解決方案：**

若要解決這兩個錯誤，請從入口網站中刪除目前的映像，然後使用與作業系統相同的設定 (一般化/特殊化) [從目前的 VHD 重新擷取映像](virtual-machines-linux-capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a>問題︰自訂/資源庫/Marketplace 映像；配置失敗
當新的 VM 要求被釘選到不支援所要求的 VM 大小、或沒有可用空間可處理要求的叢集，便會發生此錯誤。

**原因 1：** 叢集無法支援要求的 VM 大小。

**解決方式 1：**

* 以較小的 VM 大小重試要求。
* 如果無法變更要求的 VM 的大小︰
  * 停止可用性設定組中的所有 VM。
    按一下 [資源群組] > [您的資源群組] > [資源] > [您的可用性設定組] > [虛擬機器] > [您的虛擬機器] > [停止]。
  * 所有 VM 都停止後，建立所需大小的新 VM。
  * 先啟動新 VM，然後選取每個已停止的 VM 並按一下 [啟動] 。

**原因 2：** 叢集沒有可用的資源。

**解決方式 2：**

* 稍後再重試要求。
* 如果新的 VM 可以屬於不同的可用性設定組
  * 在不同的可用性設定組 (位於相同區域) 中建立新的 VM。
  * 將新的 VM 加入相同的虛擬網路。

## <a name="next-steps"></a>後續步驟
如果您在啟動已停止的 Linux VM，或重新調整 Azure 中現有的 Linux VM 大小時遇到問題，請參閱 [針對在 Azure 中重新啟動或調整現有 Linux 虛擬機器大小的 Resource Manager 部署問題進行疑難排解](virtual-machines-linux-restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。




<!--HONumber=Nov16_HO3-->


