---
title: フレンドリ名の設定、APO の登録
description: このトピックでは、ポート クラス Bluetooth 側波帯のオーディオ ドライバーが、デバイス インターフェイスの表示名を設定し、Bluetooth デバイスで使用される任意の APO を登録方法について説明します。
ms.assetid: A3C4E04C-8F3B-49B4-8E46-CF37E1A4F5AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1aa3cb6200531ecb98936cf13510e23bebe341c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355252"
---
# <a name="setting-friendly-names-registering-apos"></a>フレンドリ名の設定、APO の登録


設定のフレンドリ名を登録する APOs のトピックでは、ポート クラス Bluetooth 側波帯のオーディオ ドライバーが、デバイス インターフェイスの表示名を設定し、Bluetooth デバイスで使用されるオーディオ処理オブジェクト (APO) の登録方法について説明します。

GUID が有効な各\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS インターフェイス、オーディオ ドライバー (PortCls) を登録する PcRegisterSubdevice 関数を呼び出し、通常ポート クラスPnP デバイス サブデバイス オーディオのアダプターを表すインターフェイス。 一般的なオーディオ ドライバーの設計では、オーディオ ドライバーは、"wave"および「トポロジ」サブ デバイス、その他のポートのクラスの関数を呼び出すことによって、接続している PcRegisterSubdevice を呼び出します。

ドライバーがで説明する手順を次の「トポロジ」サブデバイス PcRegisterSubdevice を呼び出す前に[プロパティの設定とレジストリ値](setting-properties-and-registry-values.md)KSCATEGORYでインターフェイスのプロパティとレジストリ値を設定するには\_オーディオ インターフェイス クラスです。 特定のプロパティとレジストリの値は、次のセクションで説明します。

## <a name="span-iddevpkeydeviceinterfacefriendlynamespanspan-iddevpkeydeviceinterfacefriendlynamespanspan-iddevpkeydeviceinterfacefriendlynamespandevpkeydeviceinterfacefriendlyname"></a><span id="DEVPKEY_DeviceInterface_FriendlyName"></span><span id="devpkey_deviceinterface_friendlyname"></span><span id="DEVPKEY_DEVICEINTERFACE_FRIENDLYNAME"></span>DEVPKEY\_DeviceInterface\_FriendlyName


オーディオ ドライバーの送信、 [ **IOCTL\_BTHHFP\_デバイス\_取得\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_descriptor)ハンズフリー プロファイル (HFP) オーディオ ドライバーに要求します。 形式で要求された情報が返されます、 [ **BTHHFP\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthhfpddi/ns-bthhfpddi-_bthhfp_descriptor)構造体と構造体で参照される、他のデータ。 オーディオ ドライバーを呼び出して DEVPKEY を設定する IoSetDeviceInterfacePropertyData\_DeviceInterface\_FriendlyName の値に、 *FriendlyName*のフィールド、 **BTHHFP\_記述子**構造体。

オーディオ ドライバーは、とおり IoSetDeviceInterfacePropertyData にパラメーターを設定します。

-   SymbolicLinkName IoRegisterDeviceInterface から返された文字列を =

-   PropertyKey = DEVPKEY\_DeviceInterface\_FriendlyName

-   Lcid = LOCALE\_NEUTRAL

-   Flags = PLUGPLAY\_PROPERTY\_PERSISTENT

-   種類 = DEVPROP\_型\_文字列\_間接

-   Size = BTHHFP\_DESCRIPTOR.FriendlyName.Length + sizeof(UNICODE\_NULL)

-   Data = BTHHFP\_DESCRIPTOR.FriendlyName.Buffer

## <a name="span-idaporegistrationspanspan-idaporegistrationspanspan-idaporegistrationspanapo-registration"></a><span id="APO_registration"></span><span id="apo_registration"></span><span id="APO_REGISTRATION"></span>APO 登録


」の説明に従って[プロパティの設定とレジストリ値](setting-properties-and-registry-values.md)ドライバーは、デバイス インターフェイスのレジストリ値を設定できます。 APO を登録するには、オーディオ ドライバーは、デバイス インターフェイスのいくつかの値を設定します。 これらの値は、INF、APO 登録に多くの場合、設定されているものと同じと 1 つのオーディオ ドライバーから次の特定の値が変更されます。

INF ファイルの構文、APO を登録するための例を次に示します。

``` syntax
HKR,"EPFX\\0",%PKEY_FX_Association%,,%KSNODETYPE_ANY%
HKR,"EPFX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_DISCOVER_EFFECTS_APO_CLSID%
```

**注**  前のスニペットに示す構文には、APO の COM サーバーを登録するための手順が含まれていません。

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[関連するデザインのガイドライン](related-design-guidelines.md)  



