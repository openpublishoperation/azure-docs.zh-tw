---
title: "教學課程：Azure Active Directory 與 Lifesize Cloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Lifesize Cloud 之間的單一登入。"
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 75fab335-fdcd-4066-b42c-cc738fcb6513
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: jeedes
translationtype: Human Translation
ms.sourcegitcommit: dcda8b30adde930ab373a087d6955b900365c4cc
ms.openlocfilehash: 7208f872e28ce53f82cf495030fabb50557bc563


---
# <a name="tutorial-azure-active-directory-integration-with-lifesize-cloud"></a>教學課程：Azure Active Directory 與 Lifesize Cloud 整合
在本教學課程中，您會了解如何整合 Lifesize Cloud 與 Azure Active Directory (Azure AD)。

Lifesize Cloud 與 Azure AD 整合提供下列優點：

* 您可以在 Azure AD 中控制可存取 Lifesize Cloud 的人員
* 您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Lifesize Cloud (單一登入)
* 您可以在 Azure 傳統入口網站中集中管理您的帳戶

若您想了解 SaaS app 與 Azure AD 整合的更多詳細資訊，請參閱 [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。

## <a name="prerequisites"></a>必要條件
若要設定 Azure AD 與 Lifesize Cloud 整合，您需要下列項目：

* Azure AD 訂用帳戶
* 已啟用 Lifesize Cloud 單一登入的訂用帳戶

> [!NOTE]
> 若要測試本教學課程中的步驟，我們不建議使用生產環境。
> 
> 

若要測試本教學課程中的步驟，您應該遵循這些建議：

* 除非必要，否則您不應使用生產環境，。
* 如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。

## <a name="scenario-description"></a>案例描述
在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。

本教學課程中說明的案例由二個主要建置組塊組成：

1. 從資源庫新增 Lifesize Cloud
2. 設定並測試 Azure AD 單一登入

## <a name="adding-lifesize-cloud-from-the-gallery"></a>從資源庫新增 Lifesize Cloud
若要設定將 Lifesize Cloud 整合到 Azure AD 中，您需要從資源庫將 Lifesize Cloud 新增到受管理的 SaaS 應用程式清單。

**若要從資源庫新增 Lifesize Cloud，請執行下列步驟：**

1. 在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。
   
    ![Active Directory][1]
2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。
3. 若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
    ![應用程式][2]
4. 按一下頁面底部的 [新增]  。
   
    ![應用程式][3]
5. 在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。
   
    ![應用程式][4]
6. 在搜尋方塊中，輸入 **Lifesize Cloud**。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_01.png)
7. 在結果窗格中，選取 [Lifesize Cloud]，然後按一下 [完成] 以新增應用程式。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>設定並測試 Azure AD 單一登入
在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入。

若要讓單一登入能夠運作，Azure AD 必須知道 Lifesize Cloud 與 Azure AD 中互相對應的使用者。 換句話說，必須在 Azure AD 使用者與 Lifesize Cloud 中的相關使用者之間建立連結關聯性。

建立此連結關聯性的方法是指派 Azure AD 中**使用者名稱**的值做為 Lifesize Cloud 中 **Username** 的值。

若要設定及測試與 Lifesize Cloud 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：

1. **[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。
2. **[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。
3. **[建立 Lifesize Cloud 測試使用者](#creating-a-lifesize-cloud-test-user)** - 在 Lifesize Cloud 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。
4. **[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。
5. **[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。

### <a name="configuring-azure-ad-single-sign-on"></a>設定 Azure AD 單一登入
在本節中，您會在傳統入口網站中啟用 Azure AD 單一登入，然後在您的 Lifesize Cloud 應用程式中設定單一登入。

**若要使用 Lifesize Cloud 設定 Azure AD 單一登入，請執行下列步驟：**

1. 在傳統入口網站的 **Lifesize Cloud** 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。
   
    ![設定單一登入][6] 
2. 在 [您希望使用者如何登入 Lifesize Cloud] 頁面上，選取 [Azure AD 單一登入]，然後按 [下一步]。 
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_03.png) 
3. 在 [設定 App 設定]  對話方塊頁面執行下列步驟：
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_04.png) 
   
    a. 在 [登入 URL] 文字方塊中，使用以下模式輸入您的使用者用來登入 Lifesize Cloud 應用程式的 URL：**https://login.lifesizecloud.com/ls/?acs**。
   
    b. 按一下 [下一步] 
4. 在 [設定在 Litmos 單一登入] 頁面上，執行下列步驟： 
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_05.png)
   
    a. 按一下 [下載憑證]，然後將檔案儲存在您的電腦上。
   
    b. 按 [下一步] 。
5. 若要取得為您的應用程式設定的 SSO，請使用系統管理員權限登入 Lifesize Cloud 應用程式。
6. 在頁面按一下您的名稱，然後按一下 [進階設定]
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_06.png)
7. 在 [進階設定] 中，現在按一下 [SSO 組態] 連結。 這會開啟您的執行個體的 SSO 組態頁面。
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_07.png)
8. 現在設定 SSO 組態 UI 中的下列值。    
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_08.png)
   
    • 從 Azure AD 複製簽發者 URL 的值，並貼到 [識別提供者簽發者] 文字方塊。
   
    • 從 Azure AD 複製遠端登入 URL 的值，並貼到 [登入 URL] 文字方塊。
   
    • 在記事本中開啟已下載的憑證並複製憑證的內容 (不包括開頭和結尾憑證的行)，將此內容貼到 [X.509 憑證] 文字方塊。
   
    • 在 [名字] 文字方塊的 SAML 屬性對應 中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**
   
    • 在 [姓氏] 文字方塊的 SAML 屬性對應 中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**
   
    • 在 [電子郵件] 文字方塊的 SAML 屬性對應 中，輸入以下格式的值：**http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**
9. 若要檢查組態，您可以按一下 [測試] 按鈕。
   
   > [!NOTE]
   > 為使測試成功，您需要在 Azure AD 中完成組態精靈，同時提供存取權給可執行測試的使用者或群組。
   > 
   > 
10. 檢查 [啟用 SSO] 按鈕以啟用 SSO。
11. 現在按一下 [更新] 按鈕，以儲存所有設定。 這會產生 RelayState 值。 複製在文字方塊中所產生的 RelayState 值。 接下來的步驟將需要此值。
12. 在傳統入口網站中，選取單一登入設定確認，然後按 [下一步] 。
    
    ![Azure AD 單一登入][10]
13. 在 [單一登入確認] 頁面上，按一下 [完成]。  
    
    ![Azure AD 單一登入][11]
14. 現在，使用系統管理員認證登入 Azure 管理入口網站 **https://portal.azure.com**
15. 在左導覽窗格中，按一下 [更多服務]
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_09.png)
16. 搜尋 Azure Active Directory，然後按一下 [Azure Active Directory] 連結
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_10.png)
17. 您會在 [企業應用程式] 按鈕下方發現所有 SaaS 應用程式。
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_11.png)
18. 現在，按一下下一個刀鋒視窗中的 [所有應用程式] 連結
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_12.png)
19. 搜尋您要安裝 RelayState 的 Lifesize 應用程式。 
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_13.png)
20. 現在，按一下刀鋒視窗中的 [單一登入] 連結
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_14.png)
21. 您會看到 [顯示進階 URL 設定] 核取方塊。 按一下該核取方塊。
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_15.png)
22. 現在，設定應用程式的 RelayState，即在 Lifesize 應用程式的 SSO 組態頁面中看到的值。 
    
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_16.png)
23. 儲存設定。

### <a name="creating-an-azure-ad-test-user"></a>建立 Azure AD 測試使用者
在本節中，您會在傳統入口網站中建立名稱為 Britta Simon 的測試使用者。

![建立 Azure AD 使用者][20]

**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**

1. 在 **Azure 傳統入口網站**中，按一下左方瀏覽窗格的 [Active Directory]。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_09.png) 
2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。
3. 若要顯示使用者清單，請按一下頂端功能表的 [使用者] 。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_03.png) 
4. 若要開啟 [新增使用者] 對話方塊，請按一下底部工具列上的 [新增使用者]。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_04.png) 
5. 在 [告訴我們這位使用者] 對話方塊頁面上，執行下列步驟： ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_05.png) 
   
    a. 針對 [使用者類型]，選取 [您組織中的新使用者]。
   
    b. 在 [使用者名稱] 文字方塊中，輸入 **BrittaSimon**。
   
    c. 按 [下一步] 。
6. 在 [使用者設定檔] 對話方塊頁面上，執行下列步驟：![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_06.png) 
   
   a. 在 [名字] 文字方塊中，輸入 **Britta**。  
   
   b. 在 [姓氏] 文字方塊中，輸入 **Simon**。
   
   c. 在 [顯示名稱] 文字方塊中，輸入 **Britta Simon**。
   
   d. 在 [角色] 清單中選取 [使用者]。
   
   e. 按 [下一步] 。
7. 在 [取得暫時密碼] 對話方塊頁面上，按一下 [建立]。
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_07.png) 
8. 在 [取得暫時密碼]  對話方塊頁面上，執行下列步驟：
   
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-lifesize-cloud-tutorial/create_aaduser_08.png) 
   
    a. 記下 [新密碼] 的值。
   
    b. 按一下頁面底部的 [新增] 。   

### <a name="creating-an-lifesize-cloud-test-user"></a>建立 Lifesize Cloud 測試使用者
在本節中，您要在 Lifesize Cloud 中建立名為 Britta Simon 的使用者。 Lifesize Cloud 支援自動使用者佈建。 在 Azure AD 驗證成功後，使用者將自動佈建於應用程式中。 

### <a name="assigning-the-azure-ad-test-user"></a>指派 Azure AD 測試使用者
在本節中，您會將 Lifesize Cloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。

![指派使用者][200] 

**若要將 Britta Simon 指派給 Lifesize Cloud，請執行下列步驟：**

1. 在傳統入口網站中，若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
    ![指派使用者][201] 
2. 在應用程式清單中，選取 [Lifesize Cloud]。 
   
    ![設定單一登入](./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_lifesizecloud_50.png) 
3. 在頂端的功能表中，按一下 [使用者] 。
   
    ![指派使用者][203]
4. 在 [使用者] 清單中，選取 [Britta Simon] 。
5. 在底部的工具列中，按一下 [指派] 。
   
    ![指派使用者][205]

### <a name="testing-single-sign-on"></a>測試單一登入
在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。

當您在存取面板中按一下 [Lifesize Cloud] 磚時，應該會自動登入您的 Lifesize Cloud 應用程式。

## <a name="additional-resources"></a>其他資源
* [如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單](active-directory-saas-tutorial-list.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-lifesize-cloud-tutorial/tutorial_general_205.png



<!--HONumber=Dec16_HO2-->


