---
title: モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定
description: モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定
ms.assetid: 58E95326-94C4-444F-BFE2-0E7DC8112119
keywords:
- モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2b5f8d3483f58e4b3ac3171373eb0d14472e654
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571456"
---
# <a name="specify-applications-in-the-mobile-broadband-metadata-authoring-wizard"></a>モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定


デバイス アプリを Microsoft Store および特権のアプリケーションを含む、サービスのさまざまなアプリケーションを指定する をクリックして、**アプリケーション**タブ。

UWP デバイスのアプリがダウンロードされ、ユーザーが初めてデバイスを接続時にインストールします。 特権を持つアプリケーションでは、デバイスへのアクセスがあります。 それぞれ 1 つだけ指定できます。

詳細については、UWP デバイス アプリと特権を持つアプリケーションは、[Windows 8 デバイス エクスペリエンス](https://go.microsoft.com/fwlink/p/?LinkId=227312)を参照してください。

## <a name="span-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanspan-idtospecifythewindowsstoredeviceappspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>Microsoft Store デバイス アプリを指定するには


アプリを指定するには、次のフィールドに入力します。

-   **パッケージ名**します。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Name 属性の値を入力します。
-   **発行元**。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Publisher 属性の値を入力します。 この値は、PC にインストールされている発行元証明書と一致する必要があります。
-   **アプリ ID**します。 アプリケーション マニフェストの Application 要素内の ID 属性の値を入力します。

**パッケージ名**、**パブリッシャー**、および**アプリ ID**アプリの package.appxmanifest の情報は、すべて一致する必要があります。

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

## <a name="span-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanspan-idtoseethepackagenameandpublisherspanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher"></span><span id="to_see_the_package_name_and_publisher"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER"></span>パブリッシャーとパッケージの名前を表示するには


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


指定する必要な特権を持つモバイル ブロード バンド インターフェイスにアクセスする Microsoft Store デバイス アプリでは、**特権を持つアプリケーション**します。

次のフィールドに入力して特権を持つアプリケーションを指定する**特権アプリケーション**:

**注**  、次のフィールドの詳細については、[Windows 8 デバイス エクスペリエンス](https://go.microsoft.com/fwlink/p/?LinkId=242009)を参照してください。 特権のあるデバイスのインターフェイス プロパティのキーについては、[DEVPKEY\_DeviceInterface\_Restricted](https://go.microsoft.com/fwlink/p/?linkid=256362)を参照してください。

 

-   **パッケージ名**します。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Name 属性の値を入力します。
-   **発行元**。 アプリケーション マニフェストのパッケージ要素の Identity 要素の Publisher 属性の値を入力します。

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

## <a name="span-iddevicenotificationhandlerspanspan-iddevicenotificationhandlerspanspan-iddevicenotificationhandlerspandevice-notification-handler"></a><span id="Device_Notification_Handler"></span><span id="device_notification_handler"></span><span id="DEVICE_NOTIFICATION_HANDLER"></span>デバイスの通知ハンドラー


モバイル ブロード バンドのプラットフォームでは、受信して、通知を表示する MNO 管理 SMS または USSD、データ使用量が上限、海外ローミング、および残り少ないに近づいてなどの拡張機能を提供します。 データ使用量に対応するための機能を提供し、接続、切断、またはモバイル ネットワーク プロバイダーの UWP アプリでバック グラウンド イベントをローミングできます。

Windows では、Microsoft Store アプリが実行されていない場合でも、イベントへの応答でいくつかのコードを実行する UWP アプリ用のブローカー機能を提供します。 通知ハンドラーを実装する方法の詳細については、[mobile operator notifications とシステム イベントを有効にする](https://go.microsoft.com/fwlink/p/?linkid=242062)を参照してください。

 

 





