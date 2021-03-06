---
title: "Azure Active Directory 報告通知"
description: "如何使用 Azure Active Directory 報告通知找出可疑登入。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: fa8ca5940bb437c1e5c3939262db000544b04e36
ms.sourcegitcommit: 732e5df390dea94c363fc99b9d781e64cb75e220
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Azure Active Directory 報告通知
## <a name="what-reports-generate-email-notifications"></a>哪些報告會產生電子郵件通知
在此階段中，只有異常的登入活動報告會觸發電子郵件通知。

## <a name="what-is-an-irregular-sign-in"></a>什麼是「異常的登入」？
異常登入是指機器學習服務演算法已經根據結合異常登入位置和裝置的「不可能的行進」條件識別的登入活動。 這可能表示駭客已嘗試使用此帳戶進行登入。

## <a name="who-receives-the-email-notifications"></a>誰會收到電子郵件通知？
電子郵件會傳送給所有已獲指派 Active Directory Premium 授權的全域管理員。 為了確保能夠送達，我們也會將電子郵件傳送到管理員的備用電子郵件地址。 管理員應將 aad-alerts-noreply@mail.windowsazure.com 納入其安全寄件者清單中，以免遺漏電子郵件。

## <a name="how-often-are-these-emails-sent"></a>這些電子郵件的傳送頻率為何？
如果過去的 30 天內或自從最後一次傳送電子郵件後 (視何者日數較少) 發生 10 起新的異常登入活動，就會傳送本電子郵件。

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a>如何存取電子郵件中提到的報告？
當您按一下連結時，系統會將您重新導向至 Azure 傳統入口網站中的報告頁面。 若要存取報告，您必須同時是：

* 您的 Azure 訂用帳戶的管理員或共同管理員
* 目錄中的全域管理員，並獲得指派的 Active Directory Premium 授權。 如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。

## <a name="can-i-turn-off-these-emails"></a>我可以關閉這些電子郵件嗎？
是，若要關閉 Azure 傳統入口網站中異常登入的相關通知，請按一下 [設定]，然後選取 [通知] 區段之下的 [已停用]。

## <a name="whats-next"></a>後續步驟
* 想知道有哪些安全性、稽核及活動報告可用嗎？ 請查看 [Azure AD 安全性、稽核及活動報告](active-directory-view-access-usage-reports.md)
* [開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)
* [在登入和存取面板頁面加上公司商標](customize-branding.md)

