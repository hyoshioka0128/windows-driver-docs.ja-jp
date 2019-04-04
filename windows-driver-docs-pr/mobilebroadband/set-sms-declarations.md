---
title: SMS 宣言のセット
description: SMS 宣言のセット
ms.assetid: fad7fb60-eb08-43e9-bc58-afb8d6b5633c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14710d0bd2e4c8f5a769a83c57607d0873c005c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553043"
---
# <a name="set-sms-declarations"></a>SMS 宣言のセット


## <a name="span-idsmsdevicecapabilitydeclarationinpackagemanifestspanspan-idsmsdevicecapabilitydeclarationinpackagemanifestspanspan-idsmsdevicecapabilitydeclarationinpackagemanifestspansms-device-capability-declaration-in-package-manifest"></a><span id="SMS_device_capability_declaration_in_package_manifest"></span><span id="sms_device_capability_declaration_in_package_manifest"></span><span id="SMS_DEVICE_CAPABILITY_DECLARATION_IN_PACKAGE_MANIFEST"></span>パッケージ マニフェストで SMS デバイス機能の宣言


SMS を使用する UWP アプリでは、Visual Studio でパッケージ マニフェスト内の SMS 機能を宣言する必要があります。

例**package.appxmanifest**:

``` syntax
  <Capabilities>
    <DeviceCapability Name="sms" />
  </Capabilities>
```

詳細については、[アプリ機能の宣言 (UWP アプリ)](https://go.microsoft.com/fwlink/p/?linkid=317125)を参照してください。

## <a name="span-idsmsappdeclarationindevicemetadataspanspan-idsmsappdeclarationindevicemetadataspanspan-idsmsappdeclarationindevicemetadataspansms-app-declaration-in-device-metadata"></a><span id="SMS_app_declaration_in_device_metadata"></span><span id="sms_app_declaration_in_device_metadata"></span><span id="SMS_APP_DECLARATION_IN_DEVICE_METADATA"></span>デバイスのメタデータで SMS アプリの宣言


モバイル ブロード バンド デバイスにアプリを判別できます SMS メッセージを送受信するを信頼します。 これを行うには、パッケージの名前で信頼を追加します、[サービス メタデータ](service-metadata.md)次のエントリのように。

**\\Package\\SoftwareInformation\\SoftwareInfo.xml**

``` syntax
<PrivilegedApplications>
  <Package>
    <Identity Name="Microsoft.SDKSamples.SMSSendReceive.JS" Version="1.0.0.0" Publisher="CN=Contoso Corporation, O=Contoso Corporation, L=Redmond, S=Washington, C=US" />
  </Package>
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[SMS のアプリの開発](developing-sms-apps.md)

 

 






