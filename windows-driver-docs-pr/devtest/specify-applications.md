---
title: デバイス メタデータ作成ウィザードでのアプリケーションの指定
description: デバイス メタデータ作成ウィザードでのアプリケーションの指定
ms.assetid: B3ECEBF3-FBC6-45E7-9FF5-439F1CDF351F
keywords:
- デバイス メタデータ作成ウィザードでのアプリケーションの指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6be78ec70a614c626c10509cb463c0c3318b5145
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582054"
---
# <a name="specify-applications-in-the-device-metadata-authoring-wizard"></a>デバイス メタデータ作成ウィザードでのアプリケーションの指定


Microsoft Store デバイス アプリと特権を持つアプリケーションを含む、デバイスのさまざまなアプリケーションを指定できます。

UWP デバイスのアプリがダウンロードされ、ユーザーが初めてデバイスを接続時にインストールします。 特権を持つアプリケーションでは、デバイスへのアクセスがあります。 それぞれ 1 つだけ指定できます。

UWP デバイス アプリと特権を持つアプリケーションの詳細については、[Windows 8 デバイス エクスペリエンス](https://go.microsoft.com/fwlink/p/?LinkId=227312)を参照してください。

## <a name="span-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>Microsoft Store デバイス アプリを指定するには


1.  **[アプリケーション]** タブをクリックします。
2.  次のフィールドに入力します。
    -   **パッケージ名**します。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Name 属性の値を入力します。 パッケージ名入手してくださいに Microsoft Store アプリの提出を作成した後、Microsoft Store の送信プロセスにより、パッケージ名が変更されたため。 参照してください[UWP デバイス アプリのライフ サイクル](https://go.microsoft.com/fwlink/p/?linkid=246571)Microsoft Store アプリを関連付けるし、アプリ マニフェストに更新された値をコピーする方法の詳細についてはします。
    -   **発行元**。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Publisher 属性の値を入力します。 発行元名には、開発者の 1 つと同じである必要があります証明書が、パッケージと、メタデータの署名に使用します。
    -   **アプリ ID**します。 アプリケーション マニフェストの Application 要素内の ID 属性の値を入力します。
    -   **通知ハンドラー**します。 通知ハンドラーについては、[デバイス メタデータ パッケージ スキーマ リファレンス for Windows 8](https://go.microsoft.com/fwlink/p/?LinkId=226753)を参照してください。

**パッケージ名**、**パブリッシャー**、および**アプリ ID**アプリ パッケージの .appxmanifest 情報に一致する必要があります。

アプリケーション マニフェストの例を次に示します。

```
<?xml version="1.0" encoding="utf-8" ?> 
   <Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
      <Identity Name="Microsoft.SDKSamples.MoFx2App" Version="1.0.0.0" Publisher="CN=Microsoft\O=Microsoft Corp\L=Redmond\S=WA\C=US" ResourceId="NorthAmerica" /> 
   <Properties>
     <DisplayName>MoFx2App SDK Sample</DisplayName> 
     <Description>MoFx2App SDK Sample</Description> 
     <Logo>images\tile-sdk.png</Logo> 
   </Properties>
<Resources>
  <Resource Language="en-us" /> 
</Resources>
<Applications>
  <Application Id="Microsoft.SDKSamples.MoFx2App" DisplayName="MoFx2App" Logo="images\tile-sdk.png" SmallLogo="images\tile-sdk.png" EntryPointType="startPage" EntryPoint="default.html">
```

## <a name="span-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher_"></span><span id="to_see_the_package_name_and_publisher_"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER_"></span>パブリッシャーとパッケージの名前を表示するには


1.  Visual Studio でアプリ ソリューションを開きます。
2.  ソリューション エクスプ ローラーで、アプリ マニフェストをクリックします。
3.  Package.appxmanifest をダブルクリックします。
4.  **パッケージ**タブで、確認、**パッケージ名**と**パブリッシャー**フィールド。

## <a name="span-idtoseetheappidspanspan-idtoseetheappidspanspan-idtoseetheappidspanto-see-the-app-id"></a><span id="To_see_the_App_ID_"></span><span id="to_see_the_app_id_"></span><span id="TO_SEE_THE_APP_ID_"></span>アプリ ID を表示するには


1.  Visual Studio でアプリ ソリューションを開きます。
2.  ソリューション エクスプ ローラーで、アプリ マニフェストをクリックします。
3.  Package.appxmanifest を右クリックします。
4.  選択**コードを表示**します。

## <a name="span-idprivilegedapplicationsspanspan-idprivilegedapplicationsspanspan-idprivilegedapplicationsspanprivileged-applications"></a><span id="Privileged_applications"></span><span id="privileged_applications"></span><span id="PRIVILEGED_APPLICATIONS"></span>特権を持つアプリケーション


特権を持つデバイスのインターフェイスにアクセスするための Microsoft Store デバイス アプリでは、アプリを指定する必要があります**特権を持つアプリケーション**します。

次のフィールドに入力して特権を持つアプリケーションを指定する**特権アプリケーション**:

**注:**  
特権のあるデバイスのインターフェイス プロパティのキーの詳細については、[DEVPKEY\_DeviceInterface\_Restricted](https://go.microsoft.com/fwlink/p/?linkid=256362)を参照してください。



-   **パッケージ名**します。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Name 属性の値を入力します。
-   **発行元**。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Publisher 属性の値を入力します。
-   特権のアプリケーションがカスタム ドライバーにアクセスする場合は、選択**AccessCustomDriver**します。

アプリケーション マニフェスト、デバイス メタデータの作成ウィザードに入力した Id の名前、発行元、およびアプリケーション Id のフィールドの表示の例を次に示します。

```XML
<?xml version="1.0" encoding="utf-8"?>
<Package xmlns="http://schemas.microsoft.com/appx/2010/manifest">
  <Identity Name="64022FABRIKAM.FabrikamDeviceApp" Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" Version="1.0.0.0" />
  <Properties>
    <DisplayName>Fabrikam Device App</DisplayName>
    <PublisherDisplayName>Fabrikam</PublisherDisplayName>
    <Logo>Assets\storeLogo-sdk.png</Logo>
  </Properties>
  <Prerequisites>
    <OSMinVersion>6.2</OSMinVersion>
    <OSMaxVersionTested>6.2</OSMaxVersionTested>
  </Prerequisites>
  <Resources>
    <Resource Language="x-generate" />
  </Resources>
  <Applications>
    <Application Id="DeviceAppForPrinters" Executable="$targetnametoken$.exe" 
        EntryPoint="DeviceAppForPrinters.App">
      <VisualElements DisplayName="Fabrikam Device App" Logo="Assets\squareTile-sdk.png" 
         SmallLogo="Assets\smallTile-sdk.png" Description="DeviceAppForPrinters" ForegroundText="light" BackgroundColor="#00b2f0" ToastCapable="true">
        <DefaultTile ShowName="allLogos" ShortName="App4PrinterCS" WideLogo="Assets\tile-sdk.png" />
        <SplashScreen Image="Assets\splash-sdk.png" BackgroundColor="#00b2f0" />
      </VisualElements>
      <Extensions>
          <Extension Category="windows.backgroundTasks" 
             EntryPoint="Fabrikam.Printing.PrintApp.PrintNotificationHandler">
               <BackgroundTasks>
                 <Task Type="systemEvent" />
               </BackgroundTasks>
          </Extension>
          <Extension Category="windows.printTaskSettings" 
             Executable="$targetnametoken$.exe" EntryPoint="DeviceAppForPrinters.App" />
      </Extensions>
    </Application>
  </Applications>
</Package>
```

アプリケーション マニフェストのフィールドに対応するデバイス メタデータの作成ウィザードによって生成される XML 内の要素の例を次に示します。

```XML
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<SoftwareInfo xmlns="http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/SoftwareInfo">

  <DeviceCompanionApplications>
       <Package>
         <Identity Name="64022FABRIKAM.FabrikamDeviceApp" 
          Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA" />
         <Applications>
          <Application Id="DeviceAppForPrinters">
           <DeviceNotificationHandlers>
                   <DeviceNotificationHandler
                      EventID="PrintNotificationHandler"
            EventAsset="Fabrikam.Printing.PrintApp.PrintNotificationHandler" />
                </DeviceNotificationHandlers>
         </Application>
          </Applications>
       </Package>
  </DeviceCompanionApplications>

  <PrivilegedApplications>
    <Package>
         <Identity Name="64022FABRIKAM.FabrikamDeviceApp" 
              Publisher="CN=05558413-FFF6-4AA5-8176-AD43036533FA"
              AccessCustomDriver="false" />  
    </Package>
  </PrivilegedApplications>
</SoftwareInfo>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイス メタデータのスキーマ リファレンス](https://msdn.microsoft.com/library/windows/hardware/br259102)










