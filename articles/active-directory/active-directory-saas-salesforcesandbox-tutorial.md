---
title: "教學課程：Azure Active Directory 與 Salesforce 沙箱整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Salesforce Sandbox 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 90e08b9cf2feb93de4877bec9734352949896dca
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>教學課程：Azure Active Directory 與 Salesforce 沙箱整合

在本教學課程中，您會了解如何整合 Salesforce Sandbox 與 Azure Active Directory (Azure AD)。

Salesforce Sandbox 與 Azure AD 整合提供下列優點：

- 您可以在 Azure AD 中控制可存取 Salesforce Sandbox 的人員
- 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Salesforce Sandbox (單一登入)
- 您可以在 Azure 入口網站中集中管理您的帳戶

如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件

若要設定 Azure AD 與 Salesforce Sandbox 整合，您需要下列項目：

- Azure AD 訂用帳戶
- 啟用 Salesforce Sandbox 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。

若要測試本教學課程中的步驟，您應該遵循這些建議：

- 除非必要，否則請勿使用生產環境。
- 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。 本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Salesforce Sandbox
2. 設定並測試 Azure AD 單一登入

## <a name="adding-salesforce-sandbox-from-the-gallery"></a>從資源庫新增 Salesforce Sandbox
若要設定將 Salesforce Sandbox 整合到 Azure AD 中，您需要從資源庫將 Salesforce Sandbox 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Salesforce Sandbox，請執行下列步驟：**

1. 在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。 

    ![Active Directory][1]

2. 瀏覽至 [企業應用程式]。 然後移至 [所有應用程式]。

    ![應用程式][2]
    
3. 按一下對話方塊頂端的 [新增應用程式] 按鈕。

    ![應用程式][3]

4. 在搜尋方塊中，輸入 **Salesforce Sandbox**。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_search.png)

5. 在結果面板中，選取 Salesforce Sandbox，然後按一下新增 按鈕以新增應用程式。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入。

若要讓單一登入運作，Azure AD 必須知道 Salesforce Sandbox 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者和 Salesforce Sandbox 中的相關使用者之間，建立連結關聯性。

建立此連結關聯性的方法，就是將 Azure AD 中 [使用者名稱] 的值指派為 Salesforce Sandbox 中 [使用者名稱] 的值。

若要設定及測試與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Salesforce Sandbox 測試使用者](#creating-a-salesforce-sandbox-test-user)** - 使 Salesforce Sandbox 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入

在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Salesforce Sandbox 應用程式中設定單一登入。

**若要與 Salesforce Sandbox 搭配運作的 Azure AD 單一登入，請執行下列步驟：**

1. 在 Azure 入口網站的 [Salesforce Sandbox] 應用程式整合頁面上，按一下 [單一登入]。

    ![設定單一登入][4]

2. 在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。
 
    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_samlbase.png)

3. 在 [Salesforce Sandbox 網域及 URL] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_url.png)

     在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://<subdomain>.my.salesforce.com`

    > [!NOTE] 
    > 這不是真正的值。 請使用實際的登入 URL 來更新此值。請連絡 [Salesforce Sandbox 客戶支援小組](https://help.salesforce.com/support)以取得此值。


4. 如果您已為目錄中的另一個 Salesforce 沙箱執行個體設定單一登入，則也須將**識別碼**設定為具有與**登入 URL** 相同的值。 
    
    >[!Note]
    >您可以在對話方塊的 [設定應用程式 URL] 頁面上，勾選 [顯示進階設定] 核取方塊，就會出現 [識別碼] 欄位。 


5. 在 [SAML 簽署憑證] 區段上，按一下 [憑證]，然後將憑證檔案儲存在您的電腦上。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_certificate.png) 

6. 按一下 [儲存]  按鈕。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_400.png)

7. 在 [Salesforce Sandbox 組態] 區段上，按一下 [設定 Salesforce Sandbox] 以開啟 [設定登入] 視窗。 從 [快速參考] 區段中複製 [SAML 實體 ID 和 SAML 單一登入服務 URL]。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_configure.png) 
<CS>
8. 在瀏覽器中開啟新索引標籤，登入您的 Salesforce Sandbox 系統管理員帳戶。

9. 在頂端的功能表中，按一下 [安裝] 。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781024.png)
10. 在左側的導覽窗格中，按一下 安全性控制項，然後按一下單一登入設定。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781025.png)
11. 在 [單一登入設定] 區段中，執行下列步驟：![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781026.png)
     
     a.  選取 [已啟用 SAML] 。 

     b.這是另一個 C# 主控台應用程式。  按一下 [新增] 。

12. 在 [SAML 單一登入設定] 區段中，執行下列步驟：

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781027.png)

    a.在 [名稱] 文字方塊中，輸入組態的名稱 (例如：*SPSSOWAAD\_Test*)。 

    b.這是另一個 C# 主控台應用程式。 將 [SMAL 實體識別碼] 值貼到 [簽發者] 文字方塊中。

    c. 如果這是您要新增至目錄的第一個 Salesforce Sandbox 執行個體，請在 [實體識別碼] 文字方塊中，輸入 **https://test.salesforce.com**。 如果您已新增 Salesforce 沙箱的執行個體，請對 [實體識別碼] 輸入**登入 URL**，其格式如下：`http://company.my.salesforce.com`  
 
    d. 按一下 [瀏覽] 來上傳已下載的憑證。  

    e. 對於 [SAML 身分識別類型]，選取 [判斷提示包含來自使用者物件的同盟識別碼]。
 
    f. 對於 [SAML 身分識別位置]，選取 [身分識別位於 Subject 陳述式的 NameIdentifier 元素中]。

    g. 將 [單一登入服務 URL] 貼到 [識別提供者登入 URL] 文字方塊中。 

    h. SFDC 不支援 SAML 登出。  解決方法是在 [識別提供者登出 URL] 文字方塊中貼上 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'。

    i. 在 [服務提供者起始的要求繫結]，選取 [HTTP POST]。 

    j. 按一下 [儲存] 。

### <a name="enable-your-domain"></a>啟用網域
本節假設您已經建立了一個網域。  如需詳細資訊，請參閱[定義您的網域名稱](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US)。

**若要啟用您的網域，請執行下列步驟：**

1. 在左邊的導覽窗格中按一下 網域管理，然後按一下我的網域。
   
     ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781029.png)
   
   >[!NOTE]
   >請確定您的網域已正確設定。 

2. 在 [登入頁面設定] 區段中，按一下 [編輯]，然後對於 [驗證服務]，選取來自前一區段 SAML 單一登入設定的名稱，最後按一下 [儲存]。
   
   ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/IC781030.png)

一旦您設定了網域，您的使用者便應使用該網域 URL 登入至 Salesforce 沙箱。  

若要取得 URL 的值，請按一下您在上一區段中所建立的 SSO 設定檔。    

> [!TIP]
> 現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！  從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。 您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)


### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][100]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_01.png) 

2. 若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_02.png) 

3. 在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_03.png) 

4. 在 [使用者]  對話頁面上，執行下列步驟：
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-salesforcesandbox-tutorial/create_aaduser_04.png) 

    a. 在 [名稱] 文字方塊中，輸入 **BrittaSimon**。

    b.這是另一個 C# 主控台應用程式。 在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。

    c. 選取 [顯示密碼] 並記下 [密碼] 的值。

    d. 按一下 [建立] 。
 
### <a name="creating-a-salesforce-sandbox-test-user"></a>建立 Salesforce Sandbox 測試使用者

本節會在 Salesforce Sandbox 中建立名為 Britta Simon 的使用者。 Salesforce Sandbox 支援預設啟用的 Just-In-Time 佈建。
在這一節沒有您需要進行的動作項目。 如果 Salesforce Sandbox 中還沒有使用者，當您嘗試存取 Salesforce Sandbox 時，就會建立新的使用者。

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者

在本節中，您會將 Salesforce Sandbox 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 Salesforce Sandbox，請執行下列步驟：**

1. 在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。

    ![指派使用者][201] 

2. 在應用程式清單中，選取 [Salesforce Sandbox]。

    ![設定單一登入](./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_salesforcesandbox_app.png) 

3. 在左側功能表中，按一下 [使用者和群組]。

    ![指派使用者][202] 

4. 按一下 [新增] 按鈕。 然後選取 [新增指派] 對話方塊上的 [使用者和群組]。

    ![指派使用者][203]

5. 在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。

6. 按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。

7. 按一下 [新增指派] 對話方塊上的 [指派] 按鈕。
    
### <a name="testing-single-sign-on"></a>測試單一登入

如果要測試您的 SSO 設定，請開啟存取面板。 如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他資源

* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [設定使用者佈建](active-directory-saas-salesforce-sandbox-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforcesandbox-tutorial/tutorial_general_203.png

