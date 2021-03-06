---
title: 教學課程：Azure Active Directory 與 Picturepark 整合 | Microsoft Docs
description: 了解如何使用 Picturepark 搭配 Azure Active Directory 來啟用單一登入、自動佈建和更多功能！
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila

ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/26/2016
ms.author: jeedes

---
# <a name="tutorial:-azure-active-directory-integration-with-picturepark"></a>教學課程：Azure Active Directory 與 Picturepark 整合
本教學課程的目的是要示範 Azure 與 Picturepark 的整合。  
本教學課程中說明的案例假設您已經具有下列項目：

* 有效的 Azure 訂用帳戶
* Picturepark 租用戶

完成本教學課程之後，您指派給 Picturepark 的 Azure AD 使用者就能夠從您的 Picturepark 公司網站 (服務提供者起始登入)，或使用 [存取面板](active-directory-saas-access-panel-introduction.md)來單一登入應用程式。

本教學課程中說明的案例由下列建置組塊組成：

1. 啟用 Picturepark 的應用程式整合
2. 設定單一登入
3. 設定使用者佈建
4. 指派使用者

![案例](./media/active-directory-saas-picturepark-tutorial/IC795055.png "Scenario")

## <a name="enabling-the-application-integration-for-picturepark"></a>啟用 Picturepark 的應用程式整合
本節的目的是要說明如何啟用 Picturepark 的應用程式整合。

### <a name="to-enable-the-application-integration-for-picturepark,-perform-the-following-steps:"></a>若要啟用 Picturepark 的應用程式整合，請執行下列步驟：
1. 在 Azure 傳統入口網站中，按一下左方瀏覽窗格的 [Active Directory] 。
   
   ![Active Directory](./media/active-directory-saas-picturepark-tutorial/IC700993.png "Active Directory")
2. 從 [目錄]  清單中，選取要啟用目錄整合的目錄。
3. 若要開啟應用程式檢視，請在目錄檢視中，按一下頂端功能表中的 [應用程式]  。
   
   ![應用程式](./media/active-directory-saas-picturepark-tutorial/IC700994.png "Applications")
4. 按一下頁面底部的 [新增]  。
   
   ![新增應用程式](./media/active-directory-saas-picturepark-tutorial/IC749321.png "Add application")
5. 在 [欲執行動作] 對話方塊上，按一下 [從資源庫中新增應用程式]。
   
   ![從組件庫新增應用程式](./media/active-directory-saas-picturepark-tutorial/IC749322.png "Add an application from gallerry")
6. 在 [搜尋方塊] 中，輸入 **Picturepark**。
   
   ![應用程式庫](./media/active-directory-saas-picturepark-tutorial/IC795056.png "Application Gallery")
7. 在結果窗格中，選取 [Picturepark]，然後按一下 [完成] 以新增應用程式。
   
   ![Picturepark](./media/active-directory-saas-picturepark-tutorial/IC795057.png "Picturepark")

## <a name="configuring-single-sign-on"></a>設定單一登入
本節的目的是要說明如何依據 SAML 通訊協定來使用同盟，讓使用者能夠用自己在 Azure AD 中的帳戶在 Picturepark 中進行驗證。  
設定 Picturepark 的單一登入需要您從憑證抓取憑證指紋值。  
如果您不熟悉這個程序，請參閱 [如何抓取憑證的指紋值](http://youtu.be/YKQF266SAxI)。

### <a name="to-configure-single-sign-on,-perform-the-following-steps:"></a>若要設定單一登入，請執行下列步驟：
1. 在 Azure 傳統入口網站的 [Picturepark] 應用程式整合頁面上，按一下 [設定單一登入] 來開啟 [設定單一登入] 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/IC795058.png "Configure Single Sign-On")
2. 在 [您希望使用者如何登入 Picturepark] 頁面上，選取 [Microsoft Azure AD 單一登入]，然後按 [下一步]。
   
   ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/IC795059.png "Configure Single Sign-On")
3. 在 [設定應用程式 URL] 頁面的 [Picturepark 登入 URL] 文字方塊中，使用下列模式輸入您的 URL："http://company.picturepark.com"，然後按 [下一步]。
   
   ![設定應用程式 URL](./media/active-directory-saas-picturepark-tutorial/IC795060.png "Configure App URL")
4. 在 [設定在 Picturepark 單一登入] 頁面上，按一下 [下載憑證] 來下載您的憑證，然後將憑證檔案儲存在您的本機電腦中。
   
   ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/IC795061.png "Configure Single Sign-On")
5. 在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Picturepark 公司網站。
6. 在最上面的工具列中，按一下 [系統管理工具]，然後按一下 [管理主控台]。
   
   ![管理主控台](./media/active-directory-saas-picturepark-tutorial/IC795062.png "Management Console")
7. 按一下 [驗證]，然後按一下 [識別提供者]。
   
   ![驗證](./media/active-directory-saas-picturepark-tutorial/IC795063.png "Authentication")
8. 在 [識別提供者組態]  區段中，執行下列步驟：
   
   ![識別提供者組態](./media/active-directory-saas-picturepark-tutorial/IC795064.png "Identity provider configuration")
   
   1. 按一下 [新增] 。
   2. 輸入組態的名稱。
   3. 選取 [設定為預設值] 。
   4. 在 Azure 傳統入口網站中的 [設定在 Picturepark 單一登入] 對話頁面上， 複製 [SAML SSO URL] 值，然後將它貼至 [簽發者 URI] 文字方塊中。
   5. 從匯出的憑證複製 [憑證指紋] 值，然後將它貼入 [受信任簽發者憑證指紋] 文字方塊。  
      
      > [!TIP]
      > 如需詳細資訊，請參閱 [如何抓取憑證的指紋值](http://youtu.be/YKQF266SAxI)
      > 
      > 
   6. 按一下 [JoinDefaultUsersGroup] 。
   7. 若要在 [宣告] 文字方塊中設定 [Emailaddress] 屬性，請輸入 **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**。
      ![組態](./media/active-directory-saas-picturepark-tutorial/IC795065.png "組態")
   8. 按一下 [儲存] 。
9. 在 Azure 傳統入口網站上，選取單一登入設定確認，然後按一下 [完成] 來關閉 [設定單一登入] 對話方塊。
   
   ![設定單一登入](./media/active-directory-saas-picturepark-tutorial/IC795066.png "Configure Single Sign-On")

## <a name="configuring-user-provisioning"></a>設定使用者佈建
若要讓 Azure AD 使用者能夠登入 Picturepark，必須將他們佈建到 Mindflash。  
Picturepark 需以手動的方式佈建。

### <a name="to-provision-a-user-accounts,-perform-the-following-steps:"></a>若要佈建使用者帳戶，請執行下列步驟：
1. 登入您的 **Picturepark** 租用戶。
2. 在最上面的工具列中，按一下 [系統管理工具]，然後按一下 [使用者]。
   
   ![使用者](./media/active-directory-saas-picturepark-tutorial/IC795067.png "Users")
3. 在 [使用者總覽] 索引標籤中，按一下 [新增]。
   
   ![使用者管理](./media/active-directory-saas-picturepark-tutorial/IC795068.png "User management")
4. 在 [建立使用者]  對話方塊中，執行下列步驟：
   
   ![建立使用者](./media/active-directory-saas-picturepark-tutorial/IC795069.png "Create User")
   
   1. 在相關的文字方塊中，輸入您想要佈建之有效 Azure Active Directory 帳戶的 [電子郵件地址]、[密碼]、[確認密碼]、[名字]、[姓氏]、[公司]、[國家]、[郵遞區號] 及 [城市]。
   2. 選取 [語言] 。
   3. 按一下 [建立] 。

> [!NOTE]
> 您可以使用任何其他的 Picturepark 使用者帳戶建立工具或 Picturepark 提供的 API，佈建 AAD 使用者帳戶。
> 
> 

## <a name="assigning-users"></a>指派使用者
若要測試您的組態，則需指派您所允許使用您應用程式的 Azure AD 使用者，藉此授予其存取組態的權限。

### <a name="to-assign-users-to-picturepark,-perform-the-following-steps:"></a>若要指派使用者給 Picturepark，請執行下列步驟：
1. 在 Azure 傳統入口網站中建立測試帳戶。
2. 在 [Picturepark] 應用程式整合頁面上，按一下 [指派使用者]。
   
   ![指派使用者](./media/active-directory-saas-picturepark-tutorial/IC795070.png "Assign Users")
3. 選取測試使用者，按一下 [指派]，然後按一下 [是] 以確認指派。
   
   ![是](./media/active-directory-saas-picturepark-tutorial/IC767830.png "Yes")

如果要測試您的單一登入設定，請開啟存取面板。 如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](active-directory-saas-access-panel-introduction.md)。

<!--HONumber=Oct16_HO2-->


