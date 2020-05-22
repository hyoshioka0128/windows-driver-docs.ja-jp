---
title: モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定
description: モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定
ms.assetid: 58E95326-94C4-444F-BFE2-0E7DC8112119
keywords:
- モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac71728e58f7cc123f4a67c9478258770ab39159
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769522"
---
# <a name="specify-applications-in-the-mobile-broadband-metadata-authoring-wizard"></a>モバイル ブロードバンド メタデータ作成ウィザードでのアプリケーションの指定


Microsoft Store デバイスアプリや特権アプリケーションなど、サービスのさまざまなアプリケーションを指定するには、[**アプリケーション**] タブをクリックします。

UWP デバイスアプリは、ユーザーが最初にデバイスに接続したときにダウンロードされ、インストールされます。 特権のあるアプリケーションには、デバイスへの特別なアクセス権があります。 1つだけを指定できます。

## <a name="span-idto_specify_the_windows_store_device_appspanspan-idto_specify_the_windows_store_device_appspanspan-idto_specify_the_windows_store_device_appspanto-specify-the-microsoft-store-device-app"></a><span id="To_specify_the_Windows_Store_device_app"></span><span id="to_specify_the_windows_store_device_app"></span><span id="TO_SPECIFY_THE_WINDOWS_STORE_DEVICE_APP"></span>Microsoft Store デバイスアプリを指定するには


アプリを指定するには、次のフィールドに入力します。

-   **パッケージ名**。 アプリケーションマニフェストの Package 要素の Identity 要素に Name 属性の値を入力します。
-   **発行元**。 アプリケーションマニフェストの Package 要素で、Identity 要素の Publisher 属性の値を入力します。 この値は、PC にインストールされている発行元の証明書と一致している必要があります。
-   **アプリ ID**。 アプリケーションマニフェストの Application 要素に ID 属性の値を入力します。

**パッケージ名**、**発行元**、**アプリ ID**はすべて、アプリケーションパッケージ package.appxmanifest の情報と一致している必要があります。

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

## <a name="span-idto_see_the_package_name_and_publisherspanspan-idto_see_the_package_name_and_publisherspanspan-idto_see_the_package_name_and_publisherspanto-see-the-package-name-and-publisher"></a><span id="To_see_the_Package_name_and_Publisher"></span><span id="to_see_the_package_name_and_publisher"></span><span id="TO_SEE_THE_PACKAGE_NAME_AND_PUBLISHER"></span>パッケージ名と発行元を表示するには


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


Microsoft Store デバイスアプリが特権のあるモバイルブロードバンドインターフェイスにアクセスするには、[特権のある**アプリケーション**] で指定する必要があります。

特権のあるアプリケーションを指定するには、[**特権アプリケーション**] の下の次のフィールドに入力します。

**メモ**   Privileged Device Interface プロパティキーの詳細については、「 [DEVPKEY \_ deviceinterface \_ Restricted](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceinterface-restricted)」を参照してください。

 

-   **パッケージ名**。 アプリケーションマニフェストの Package 要素の Identity 要素に Name 属性の値を入力します。
-   **発行元**。 アプリケーションマニフェストの Package 要素で、Identity 要素の Publisher 属性の値を入力します。

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

## <a name="span-iddevice_notification_handlerspanspan-iddevice_notification_handlerspanspan-iddevice_notification_handlerspandevice-notification-handler"></a><span id="Device_Notification_Handler"></span><span id="device_notification_handler"></span><span id="DEVICE_NOTIFICATION_HANDLER"></span>デバイス通知ハンドラー


モバイルブロードバンドプラットフォームは、データ使用量の上限、国際ローミング、低残高など、MNO の管理 SMS または USSD 通知を受信して表示するための拡張機能を提供します。 また、モバイルネットワークプロバイダーの UWP アプリで、データの使用状況や接続、切断、ローミングのバックグラウンドイベントに応答するための機能も提供します。

Windows には、Microsoft Store アプリが実行されていない場合でも、イベントに応答してコードを実行するための UWP アプリのブローカー機能が用意されています。 通知ハンドラーの実装の詳細については、「[モバイルオペレーター通知とシステムイベントの有効化の概要](https://docs.microsoft.com/windows-hardware/drivers/mobilebroadband/enabling-mobile-operator-notifications-and-system-events)」を参照してください。

 

 





