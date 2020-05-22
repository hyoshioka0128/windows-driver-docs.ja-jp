---
title: デバイス メタデータ作成ウィザードでのアプリケーションの指定
description: デバイス メタデータ作成ウィザードでのアプリケーションの指定
ms.assetid: B3ECEBF3-FBC6-45E7-9FF5-439F1CDF351F
keywords:
- デバイス メタデータ作成ウィザードでのアプリケーションの指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3498cc6c1979dd7edfd47e21f1a1c389bae26aa9
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769510"
---
# <a name="specify-applications-in-the-device-metadata-authoring-wizard"></a>デバイス メタデータ作成ウィザードでのアプリケーションの指定


デバイスのさまざまなアプリケーション (Microsoft Store デバイスアプリや特権アプリケーションなど) を指定できます。

UWP デバイスアプリは、ユーザーが最初にデバイスに接続したときにダウンロードされ、インストールされます。 特権のあるアプリケーションには、デバイスへの特別なアクセス権があります。 1つだけを指定できます。

## <a name="span-idto_specify_the_windows_store_device_appspanspan-idto_specify_the_windows_store_device_appspanspan-idto_specify_the_windows_store_device_appspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>Microsoft Store デバイスアプリを指定するには


1.  **[アプリケーション]** タブをクリックします。
2.  次のフィールドに入力します。
    -   **パッケージ名**。 アプリケーションマニフェストの Package 要素の Identity 要素に Name 属性の値を入力します。 パッケージ名は、Microsoft Store の送信プロセスによって変更されるため、Microsoft Store へのアプリの送信後に取得する必要があります。 アプリを Microsoft Store に関連付け、更新された値をアプリマニフェストにコピーする方法の詳細については、「 [UWP デバイスアプリのビルド](https://docs.microsoft.com/windows-hardware/drivers/devapps/the-workflow)」を参照してください。
    -   **発行元**。 アプリケーションマニフェストの Package 要素で、Identity 要素の Publisher 属性の値を入力します。 発行元の名前は、パッケージとメタデータの署名に使用される開発者証明書の名前と同じである必要があります。
    -   **アプリ ID**。 アプリケーションマニフェストの Application 要素に ID 属性の値を入力します。
    -   **通知ハンドラー**。 通知ハンドラーの詳細については、「[デバイスメタデータスキーマリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541452(v=vs.85))」を参照してください。

**パッケージ名**、**発行元**、**アプリ ID**は、アプリケーションパッケージ package.appxmanifest の情報と一致する必要があります。

アプリケーションマニフェストの例を次に示します。

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

## <a name="span-idto_see_the_package_name_and_publisher_spanspan-idto_see_the_package_name_and_publisher_spanspan-idto_see_the_package_name_and_publisher_spanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher_"></span><span id="to_see_the_package_name_and_publisher_"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER_"></span>パッケージ名と発行元を表示するには


1.  Visual Studio でアプリ ソリューションを開きます。
2.  ソリューションエクスプローラーでアプリケーションマニフェストをクリックします。
3.  Package.appxmanifest をダブルクリックします。
4.  [パッケージ**化**] タブで、**パッケージ名**と**発行元**フィールドを確認します。

## <a name="span-idto_see_the_app_id_spanspan-idto_see_the_app_id_spanspan-idto_see_the_app_id_spanto-see-the-app-id"></a><span id="To_see_the_App_ID_"></span><span id="to_see_the_app_id_"></span><span id="TO_SEE_THE_APP_ID_"></span>アプリ ID を表示するには


1.  Visual Studio でアプリ ソリューションを開きます。
2.  ソリューションエクスプローラーでアプリケーションマニフェストをクリックします。
3.  Package.appxmanifest を右クリックします。
4.  [**コードの表示**] を選択します。

## <a name="span-idprivileged_applicationsspanspan-idprivileged_applicationsspanspan-idprivileged_applicationsspanprivileged-applications"></a><span id="Privileged_applications"></span><span id="privileged_applications"></span><span id="PRIVILEGED_APPLICATIONS"></span>特権のあるアプリケーション


Microsoft Store デバイスアプリが特権のあるデバイスインターフェイスにアクセスできるようにするには、[**特権**のあるアプリケーション] でアプリを指定する必要があります。

特権のあるアプリケーションを指定するには、[**特権アプリケーション**] の下の次のフィールドに入力します。

**注**  
Privileged Device Interface プロパティキーの詳細については、「 [DEVPKEY \_ deviceinterface \_ Restricted](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceinterface-restricted)」を参照してください。



-   **パッケージ名**。 アプリケーションマニフェストの Package 要素の Identity 要素に Name 属性の値を入力します。
-   **発行元**。 アプリケーションマニフェストの Package 要素で、Identity 要素の Publisher 属性の値を入力します。
-   特権のあるアプリケーションがカスタムドライバーにアクセスする場合は、[ **Accesscustomdriver**] を選択します。

次に、デバイスメタデータ作成ウィザードに入力された Id 名、発行元、およびアプリケーション Id のフィールドを示すアプリケーションマニフェストの例を示します。

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

次に、アプリケーションマニフェストのフィールドに対応する、デバイスメタデータ作成ウィザードによって生成される XML の要素の例を示します。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[デバイスメタデータスキーマのリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))










