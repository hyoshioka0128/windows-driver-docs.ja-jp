---
title: フレンドリ名の設定、APO の登録
description: このトピックでは、Port Class Bluetooth sideband audio driver がデバイスインターフェイスのフレンドリ名を設定し、Bluetooth デバイスで使用されている APO を登録する方法について説明します。
ms.assetid: A3C4E04C-8F3B-49B4-8E46-CF37E1A4F5AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5df16c68791aab1470f906f25a3b0565fdc01dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830125"
---
# <a name="setting-friendly-names-registering-apos"></a>フレンドリ名の設定、APO の登録


[フレンドリ名の設定]、[APOs topic の登録] で、ポートクラスの Bluetooth sideband audio driver がデバイスインターフェイスのフレンドリ名を設定する方法と、Bluetooth デバイスで使用されるオーディオ処理オブジェクト (APO) を登録する方法について説明します。

有効な GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスインターフェイスに対して、ポートクラスオーディオドライバー (PortCls) は通常、Pcregiのサブデバイス関数を呼び出します。これにより、PnP デバイスインターフェイスが登録されます。オーディオアダプターのサブデバイスを表します。 一般的なオーディオドライバーの設計では、オーディオドライバーは "wave" サブデバイスと "トポロジ" サブデバイスに対して Pcregiを呼び出し、その後、他のポートクラス関数を呼び出して接続します。

"トポロジ" サブデバイスに対して PcregiKSCATEGORY サブデバイスを呼び出す前に、ドライバーは、「[プロパティとレジストリ値の設定](setting-properties-and-registry-values.md)」で説明されている手順に従って、\_インターフェイスのプロパティとレジストリ値を設定します。講義. 以下のセクションでは、特定のプロパティとレジストリ値について説明します。

## <a name="span-iddevpkey_deviceinterface_friendlynamespanspan-iddevpkey_deviceinterface_friendlynamespanspan-iddevpkey_deviceinterface_friendlynamespandevpkey_deviceinterface_friendlyname"></a><span id="DEVPKEY_DeviceInterface_FriendlyName"></span><span id="devpkey_deviceinterface_friendlyname"></span><span id="DEVPKEY_DEVICEINTERFACE_FRIENDLYNAME"></span>DEVPKEY\_DeviceInterface\_FriendlyName


オーディオドライバーは、ハンドフリープロファイル (HFP) オーディオドライバーに[ **\_記述子要求を取得\_、IOCTL\_BTHHFP\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)に送信します。 要求された情報は、 [**Bthhfp\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)の構造体と、構造体によって参照されるその他のデータの形式で返されます。 次に、オーディオドライバーは IoSetDeviceInterfacePropertyData を呼び出して、DEVPKEY\_DeviceInterface\_FriendlyName を**Bthhfp\_記述子**構造体の*friendlyname*フィールドの値に設定します。

オーディオドライバーは、次のように、パラメーターを IoSetDeviceInterfacePropertyData に設定します。

-   SymbolicLinkName = IoRegisterDeviceInterface から返される文字列

-   PropertyKey = DEVPKEY\_DeviceInterface\_FriendlyName

-   Lcid = ロケール\_ニュートラル

-   Flags = PLUGPLAY\_プロパティ\_PERSISTENT

-   Type = DEVPROP\_TYPE\_STRING\_間接

-   Size = BTHHFP\_記述子。FriendlyName. Length + sizeof (UNICODE\_NULL)

-   データ = BTHHFP\_記述子。FriendlyName. Buffer

## <a name="span-idapo_registrationspanspan-idapo_registrationspanspan-idapo_registrationspanapo-registration"></a><span id="APO_registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 登録


「[プロパティとレジストリ値の設定](setting-properties-and-registry-values.md)」で説明されているように、ドライバーはデバイスインターフェイスのレジストリ値を設定できます。 APO を登録するために、オーディオドライバーはデバイスインターフェイスに複数の値を設定します。 これらの値は、INF での APO 登録に対して設定されることが多い値と同じであり、特定の値が1つのオーディオドライバーから次のドライバーに変更されます。

APO を登録するための INF ファイル構文の例を次に示します。

``` syntax
HKR,"EPFX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"EPFX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
```

前のスニペットに示されている構文には、APO の COM サーバーを登録するための手順が含まれていない**ことに注意**してください  。

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[関連するデザインガイドライン](related-design-guidelines.md)  



