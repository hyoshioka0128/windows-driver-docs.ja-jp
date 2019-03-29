---
title: プロパティとレジストリ値の設定
description: プロパティの設定とレジストリ値のトピックでは、ポート クラス オーディオ ドライバーのプロパティと PnP デバイス インターフェイスのレジストリ値に設定する方法について説明します。
ms.assetid: EB6E9673-4A87-45D9-A334-8C2AE33A7581
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143c95f099afeb8b40c6df1e5c5d7eb7ab51fb2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572925"
---
# <a name="setting-properties-and-registry-values"></a>プロパティとレジストリ値の設定


プロパティの設定とレジストリ値のトピックでは、ポート クラス オーディオ ドライバーのプロパティと PnP デバイス インターフェイスのレジストリ値に設定する方法について説明します。

ポート クラスのオーディオ ドライバー Portcls は正しく、デバイス インターフェイスを登録し、必要な値を設定するには、次の手順を実行する必要があります。

## <a name="span-id1registerthedeviceinterfacespanspan-id1registerthedeviceinterfacespan1-register-the-device-interface"></a><span id="1._register_the_device_interface"></span><span id="1._REGISTER_THE_DEVICE_INTERFACE"></span>1.登録、デバイス インターフェイス


PcRegisterSubdevice サブのデバイスを呼び出す前に、ドライバーは直接、KSCATEGORY を登録する IoRegisterDeviceInterface を呼び出す\_オーディオ インターフェイス。 これは、方法により、ドライバーは、登録し、インターフェイスを有効に PcRegisterSubdevice 前に、デバイス インターフェイスのインターフェイスのプロパティとレジストリ値を設定します。

オーディオ ドライバーは、次のように IoRegisterDeviceInterface のパラメーターを設定します。

-   PhysicalDeviceObject パラメーターは、PDEVICE\_PcGetPhysicalDeviceObject 関数から、オーディオ ドライバーを取得できるオブジェクト。

-   InterfaceClassGuid は、インターフェイスのクラス GUID に設定されます。

-   ReferenceString では、オーディオ ドライバーに渡します PcRegisterSubdevice Name パラメーターと同じです。

前のタスクが正常に完了、IoRegisterDeviceInterface は登録されているインターフェイスの SymbolicLinkName を返します。

## <a name="span-id2setregistryvaluesspanspan-id2setregistryvaluesspan2-set-registry-values"></a><span id="2._set_registry_values"></span><span id="2._SET_REGISTRY_VALUES"></span>2.レジストリ値の設定


オーディオ ドライバーでは、デバイス インターフェイスのレジストリ キーを識別するハンドルを取得する IoOpenDeviceInterfaceRegistryKey を呼び出します。 オーディオ ドライバーは、次のように IoOpenDeviceInterfaceRegistryKey にパラメーターを設定します。

SymbolicLinkName は、前の手順で IoRegisterDeviceInterface から返される文字列です。

キーに設定されている、DesiredAccess\_書き込み (またはその他の値をドライバーが必要な場合)。

上記の手順が正常に完了したら、DeviceInterfaceKey は開かれているレジストリ キー ハンドルを返します。 オーディオ ドライバー:

-   レジストリ値を設定する呼び出し ZwSetValueKey

-   ZwClose を呼び出すことによって、レジストリ キー ハンドルを終了します。

**注**  をドライバーがレジストリ サブキーで値を設定する必要がある場合、ドライバーを呼び出して ZwCreateKey サブキーを作成します。 ZwCreateKey、ドライバーの呼び出しの準備: 場合
-   InitializeObjectAttributes を呼び出すし、オブジェクト名をサブキーのパスに設定

-   OBJ 属性を設定します\_ケース\_INSENSITIVE |OBJ\_カーネル\_処理

-   RootDirectory を IoOpenDeviceInterfaceRegistryKey によって返されたハンドルに設定します。

-   呼び出す ZwClose ZwCreateKey を呼び出すことによって作成されたいずれかのハンドルを閉じる

 

## <a name="span-id3setpropertiesspanspan-id3setpropertiesspan3-set-properties"></a><span id="3._set_properties"></span><span id="3._SET_PROPERTIES"></span>3.プロパティの設定


オーディオ ドライバーでは、プロパティを設定する IoSetDeviceInterfacePropertyData を呼び出します。 オーディオ ドライバーは、とおり IoSetDeviceInterfacePropertyData にパラメーターを設定します。 
- SymbolicLinkName は、IoRegisterDeviceInterface から返される文字列です。 
- 残りのパラメーターは、設定されている特定のプロパティによって異なります。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[関連するデザインのガイドライン](related-design-guidelines.md)  



