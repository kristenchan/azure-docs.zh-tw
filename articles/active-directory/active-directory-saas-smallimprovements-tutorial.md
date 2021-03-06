---
title: "教學課程：Azure Active Directory 與 Small Improvements 整合| Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Small Improvements 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 49a8cd3acfc6df15ef6a51171c8421162bc94efc
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a>教學課程：Azure Active Directory 與 Small Improvements 整合

在本教學課程中，您將了解如何整合 Small Improvements 與 Azure Active Directory (Azure AD)。

Small Improvements 與 Azure AD 整合提供下列優點：

- 您可在 Azure AD 中控制可存取 Small Improvements 的人員
- 您可以讓使用者使用其 Azure AD 帳戶自動登入 Small Improvements (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Small Improvements 的整合作業，需要下列項目：

- Azure AD 訂用帳戶
- 已啟用 Small Improvements 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Small Improvements
2. 設定並測試 Azure AD 單一登入

## <a name="adding-small-improvements-from-the-gallery"></a>從資源庫新增 Small Improvements
若要設定 Small Improvements 與 Azure AD 的整合作業，您需要從資源庫將 Small Improvements 新增至受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Small Improvements，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Small Improvements**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_search.png)

5. 在結果窗格中，選取 Small Improvements，然後按一下新增 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Small Improvements 搭配運作的 Azure AD 單一登入。

若要讓單一登入作用，Azure AD 必須知道 Small Improvements 與 Azure AD 中互相對應的使用者。 換句話說，必須建立 Azure AD 使用者和 Small Improvements 中相關使用者之間的連結關聯性。

在 Small Improvements 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。

若要使用 Small Improvements 設定及測試 Azure AD 單一登入功能，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Small Improvements 測試使用者](#creating-a-small-improvements-test-user)** - 使 Small Improvements 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Small Improvements 應用程式中設定單一登入。

**若要使用 Small Improvements 設定 Azure AD 單一登入功能，請執行下列步驟：**

1. 在 Azure 入口網站的 [Small Improvements] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_samlbase.png)

3. 在 [Small Improvements 網域與 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_url.png)

    a. 在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.small-improvements.com`

    b. 在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.small-improvements.com`

    > [!NOTE] 
    > 這些都不是真正的值。 使用實際的「登入 URL」及「識別碼」來更新這些值。 請連絡 [Small Improvements 客戶支援小組](mailto:support@small-improvements.com)以取得這些值。 
 
4. 在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_certificate.png) 

5. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_400.png)

6. 在 [Small Improvements 組態] 區段上，按一下 [設定 Small Improvements] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_configure.png) 

7. 在另一個瀏覽器視窗中，以系統管理員身分登入您的 Small Improvements 公司網站。

8. 在主要儀表板頁面上，按一下左側的 [系統管理]  按鈕。
   
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 

9. 按一下 [整合] 區段的 [SAML SSO] 按鈕。
   
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 

10. 在 [SSO 設定] 頁面上，執行下列步驟：
   
    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  

    a. 在 [HTTP 端點] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。

    b.這是另一個 C# 主控台應用程式。 在記事本中開啟您下載的憑證，然後複製憑證內容，再把該內容貼到 [x509 憑證] 文字方塊中。 

    c. 如果您想讓使用者能夠使用 SSO 和登入表單驗證，請選取 [啟用也能透過登入/密碼來存取] 選項。  

    d. 在 [SAML 提示] 文字方塊中，輸入適當的值來為 SSO 登入按鈕命名。  

    e. 按一下 [儲存] 。

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_02.png) 

3. 若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-small-improvements-test-user"></a>建立 Small Improvements 的測試使用者

若要讓 Azure AD 使用者能夠登入 Small Improvements，必須將他們佈建到 Small Improvements。 Small Improvements 需以手動的方式佈建。

**若要佈建使用者帳戶，請執行下列步驟：**

1. 以系統管理員身分登入您的 Small Improvements 公司網站。

2. 按一下首頁左側功能表中的 [系統管理] 。

3. 按一下 [使用者管理] 區段的 [使用者目錄]  按鈕。 
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 

4. 按一下 [新增使用者]。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png) 

5. 在 [新增使用者] 對話方塊上，執行下列步驟： 

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)
    
    a. 輸入使用者的**名字**，例如 **Britta**。

    b.這是另一個 C# 主控台應用程式。 輸入使用者的**姓氏**，例如 **Simon**。

    c. 輸入使用者的**電子郵件**，例如 **brittasimon@contoso.com**。 

    d. 您也可以選擇在 [傳送通知電子郵件]  方塊中，輸入您個人的訊息。 如果您不想傳送通知，則取消選取此核取方塊。

    e. 按一下 [建立使用者] 。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Small Improvements 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派到 Small Improvements，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Small Improvements] 。

    ![設定單一登入](./media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。  

當您在存取面板中按一下 [Small Improvements] 磚時，應該會自動登入 Small Improvements 應用程式。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png

