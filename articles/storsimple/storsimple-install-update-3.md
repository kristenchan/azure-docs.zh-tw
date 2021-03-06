---
title: "在 StorSimple 裝置上安裝 Update 3 | Microsoft Docs"
description: "說明如何在您的 StorSimple 8000 系列裝置上安裝「StorSimple 8000 系列 Update 3」。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/03/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2b99b9cd52dd28f7f62b5d8d5ffe32339a67f82a
ms.sourcegitcommit: 0930aabc3ede63240f60c2c61baa88ac6576c508
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>在 StorSimple 8000 系列裝置上安裝 Update 3

> [!NOTE]
> StorSimple 的傳統入口網站已過時。 按照淘汰排程，StorSimple 裝置管理員會自動移至新的 Azure 入口網站。 您將收到關於此移動的電子郵件和入口網站通知。 本文件也很快就會淘汰。 若有關於移動的任何問題，請參閱[常見問題集：移至 Azure 入口網站](storsimple-8000-move-azure-portal-faq.md)。


## <a name="overview"></a>概觀

本教學課程說明如何透過 Azure 傳統入口網站及使用 Hotfix 方法，在執行舊軟體版本的 StorSimple 裝置上安裝 Update 3。 當閘道器是設定於 StorSimple 裝置之 DATA 0 以外的網路介面上，且您正嘗試從 Update 1 以前的軟體版本更新時，就會使用 Hotfix 方法。

Update 3 包含裝置軟體、LSI 驅動程式和韌體以及 Storport 和 Spaceport 的更新。 如果是從 Update 2 或更舊的版本更新，系統也會要求您套用 iSCSI、WMI 更新，以及在某些情況下必須套用磁碟韌體更新。 裝置軟體、WMI、iSCSI、LSI 驅動程式、Spaceport 和 Storport 修正程式是非干擾性更新。 這些更新可以透過 Azure 傳統入口網站套用。 磁碟韌體更新為干擾性更新，且只能透過裝置的 Windows PowerShell 介面套用。

> [!IMPORTANT]
> * 安裝前會執行一組手動和自動預先檢查，以根據硬體狀態和網路連線來判斷裝置健全狀況。 這些預先檢查只會在您從 Azure 傳統入口網站套用更新時執行。
> * 建議您透過 Azure 傳統入口網站安裝軟體和驅動程式更新。 只在入口網站中的更新前閘道檢查失敗時，才移至裝置的 Windows PowerShell 介面以安裝更新。 視您從哪一個版本更新而定，可能需要 1.5-2.5 小時來安裝更新。 維護模式更新必須透過裝置的 Windows PowerShell 介面安裝。 由於維護模式更新是干擾性更新，所以您的裝置會發生停機。
> * 如果執行選擇性的 StorSimple Snapshot Manager，更新裝置之前，請先將您的 Snapshot Manager 版本升級至 Update 2。

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-the-azure-classic-portal"></a>透過 Azure 傳統入口網站安裝 Update 3
請執行下列步驟來將您的裝置更新至 [Update 3](storsimple-update3-release-notes.md)。

> [!NOTE]
> 如果您是要套用 Update 2 或更新版本 (包括 Update 2.1)，Microsoft 將可以提取裝置的其他診斷資訊。 這項資料可協助識別有問題的 StorSimple 裝置，並協助診斷問題。 接受 Update 2 或更新版本，表示您允許我們提供此主動支援。


[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

確認您裝置執行的是 **StorSimple 8000 系列 Update 3 (6.3.9600.17759)**。 **上次更新日期**已修改。 
   - 如果要從 Update 2 之前的版本更新，則您會看到有維護模式更新可以使用。 安裝更新後，可能會繼續顯示此訊息最多 24 小時。
     維護模式更新是導致裝置停機的干擾性更新。 這些更新只能透過裝置的 Windows PowerShell 介面套用。 在某些情況下，當您執行 Update 1.2 時，磁碟韌體可能已經是最新狀態，您不需要安裝任何維護模式更新。
   - 如果您是從 Update 2 或更新版本進行更新，您的裝置現在應該已是最新狀態。 您可以略過下一個步驟。

下載維護模式更新，方法是使用 [下載 Hotfix](#to-download-hotfixes) 中列出的步驟來搜尋和下載 KB3121899，它會安裝磁碟韌體更新 (此時應該已經安裝其他更新)。 請遵循 [安裝及驗證維護模式 Hotfix](#to-install-and-verify-maintenance-mode-hotfixes) 中列出的步驟安裝維護模式更新。 

## <a name="install-update-3-as-a-hotfix"></a>以 Hotfix 方式安裝 Update 3
請在嘗試透過 Azure 傳統入口網站安裝更新，而無法通過閘道器檢查時執行此程序。 當您指派閘道器給非 DATA 0 網路介面且您的裝置正在執行早於 Update 1 的軟體版本時，檢查才會失敗。

可以使用 Hotfix 方法升級的軟體版本為：

* Update 0.1、0.2、0.3
* Update 1、1.1、1.2
* Update 2、2.1、2.2 

> [!IMPORTANT]
> * 如果您的裝置正在執行 Release (GA) 版本，請連絡 [Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以協助您進行更新。
> 
> 

Hotfix 方法涉及下列三個步驟：

1. 從 Microsoft Update Catalog 下載 Hotfix。
2. 安裝及驗證定期模式 Hotfix。
3. 安裝並確認維護模式 Hotfix (僅限於從 Update 2 之前的軟體更新時)。

#### <a name="download-updates-for-your-device"></a>下載適用於您裝置的更新
**如果您裝置執行的是 Update 2.1 或 2.2**，您就必須依指定的順序下載並安裝下列 Hotfix：

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |軟體更新 &#42; |定期  <br></br>非干擾性 |~ 45 分鐘 |
| 2. |KB3186859 |LSI 驅動程式與韌體 |定期  <br></br>非干擾性 |~ 20 分鐘 |
| 3. |KB3121261 |Storport 和 Spaceport 修正程式  </br> Windows Server 2012 R2 |定期  <br></br>非干擾性 |~ 20 分鐘 |

&#42;  *請注意，軟體更新是由兩個二進位檔組成︰開頭為 `all-hcsmdssoftwareupdate` 的裝置軟體更新，以及開頭為 `all-cismdsagentupdatebundle` 的 Cis 和 Mds 代理程式。必須先安裝裝置軟體更新，再安裝 Cis 和 Mds 代理程式。您還必須在套用 Cis 和 MDS 代理程式更新之後，先透過 `Restart-HcsController` Cmdlet 重新啟動作用中的控制器，然後才套用剩餘的更新。* 

**如果您裝置執行的是 Update 0.1、0.2、0.3、1.0、1.1、1.2 或 2.0**，則除了軟體、LSI 驅動程式及韌體更新 (如前一個表格所示) 之外，您還必須依指定的順序下載並安裝下列 Hotfix：

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |iSCSI 封裝 |定期  <br></br>非干擾性 |~ 20 分鐘 |
| 5. |KB3103616 |WMI 封裝 |定期  <br></br>非干擾性 |~ 12 分鐘 |

<br></br>

**如果您裝置執行的版本是 0.2、0.3、1.0、1.1 及 1.2**，則除了前面表格所示的所有更新之外，您可能還需要安裝磁碟韌體更新。 您可以執行 `Get-HcsFirmwareVersion` Cmdlet 來確認是否需要進行磁碟韌體更新。 如果您執行的是這些韌體版本：`XMGG`、`XGEG`、`KZ50`、`F6C2`、`VR08`，您就不需要安裝這些更新。

| 順序 | KB | 說明 | 更新類型 | 安裝時間 |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |磁碟韌體 |維護  <br></br>干擾性 |~ 30 分鐘 |

<br></br>

> [!IMPORTANT]
> * 此程序僅需要執行一次，即可套用 Update 3。 您可以使用 Azure 傳統入口網站套用後續的更新。
> * 如果您是從 Update 2.2 進行更新，則總安裝時間會接近 1.1 小時。
> * 使用此程序套用更新之前，請確定兩個裝置控制器都在線上，而且所有硬體元件的狀況良好。
> 
> 

請執行以下步驟來下載及安裝 Hotfix。

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>後續步驟
深入了解 [Update 3 版](storsimple-update3-release-notes.md)。

