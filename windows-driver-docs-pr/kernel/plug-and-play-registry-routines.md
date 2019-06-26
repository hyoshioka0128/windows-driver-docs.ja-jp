---
title: プラグ アンド プレイ レジストリ ルーチン
description: プラグ アンド プレイ レジストリ ルーチン
ms.assetid: d526af4e-8b33-46fb-9af9-b0d9b9f1913a
keywords:
- レジストリの WDK カーネル、プラグ アンド プレイ
- ドライバーのレジストリ情報 WDK カーネル、プラグ アンド プレイ
- プラグ アンド プレイ WDK カーネルでは、レジストリのルーチン
- ハードウェア キー WDK カーネル
- ソフトウェア キー WDK カーネル
- IoOpenDeviceRegistryKey
- IoOpenDeviceInterfaceRegistryKey
- PnP WDK カーネルでは、レジストリのルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f6398915c4afd1becf4ec4871614fc8d09fc30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380938"
---
# <a name="plug-and-play-registry-routines"></a>プラグ アンド プレイ レジストリ ルーチン


プラグ アンド プレイ マネージャーは、ドライバー、そのデバイス、およびそのデバイス インターフェイスのインスタンスを特定のレジストリ キーを関連付けます。 ドライバーは、これらのキーを使用して、ドライバー、または特定のデバイスまたはデバイス インターフェイスのインスタンスに関連付けられた永続的なプロパティを格納できます。

ドライバーは、これらのキーを直接アクセスする必要があることはありません。 Windows の将来のバージョン可能性があります、または情報を格納別の場所にレジストリで、レジストリ外全体。 ドライバーは、次のツリー内のすべてのキーを直接アクセスできないする必要があります。

-   HKLM\\システム\\CurrentControlSet\\コントロール\\クラス

-   HKLM\\システム\\CurrentControlSet\\コントロール\\DeviceClasses

-   HKLM\\システム\\CurrentControlSet\\列挙型

-   HKLM\\システム\\CurrentControlSet\\ハードウェア プロファイル

代わりに、ドライバーを使用して、 [ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)と[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)ルーチンの PnP にアクセスするにはキー。

PnP マネージャーでは、ドライバーの場合、ドライバーのソフトウェアのキー、および各デバイスの場合、デバイスのハードウェア キーと呼ばれるキーと呼ばれる 1 つのキーを割り当てます。 **IoOpenDeviceRegistryKey**ルーチンがいずれかのキーを開くことができます。 値、 *DevInstKeyType*を開くには、どのキーを指定します。 PLUGPLAY を指定\_REGKEY\_ドライバー、ソフトウェア キーまたは PLUGPLAY を開く\_REGKEY\_ハードウェア キーへのデバイス。 *デバイス オブジェクト*パラメーターは、デバイスまたはドライバーを指定します。 (ドライバーは、and 演算 PLUGPLAY によって、現在のハードウェア プロファイルを基準とそのハードウェアとソフトウェア キーにもアクセスできます\_REGKEY\_現在\_に HWPROFILE *DevInstKeyType*)。

**IoOpenDeviceInterfaceRegistryKey**特定のデバイス インターフェイスのインスタンスに関連付けられたキーを開きます。 これは、その名前で、インスタンスが識別される、 [ **UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)によって返される[ **IoGetDeviceInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfaces)、[ **IoGetDeviceInterfaceAlias**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceinterfacealias)、または[ **IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)します。 として文字列が渡される、 *SymbolicLinkValue*パラメーターを**IoOpenDeviceInterfaceRegistryKey**します。

INF ファイル、またはを使用して、これらのキーを設定することも、 **SetupDi * Xxx*** ルーチン。 詳細については、次を参照してください。[ドライバーのレジストリ キー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)します。

両方[ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)と[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)としてアクセス権を持つ、開いているキー ハンドルを提供指定された、 *DesiredAccess*パラメーター。 ドライバーを使用して、その後、 **Zw * Xxx*** レジストリのルーチンなど[ **ZwQueryValueKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwqueryvaluekey)と[ **ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwsetvaluekey)にアクセスして、キーを操作します。 ドライバーが呼び出すことによって、ハンドルを閉じ、ドライバーは不要になったハンドルを使用して後、 [ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)します。 詳細については、次を参照してください。[レジストリ キー オブジェクトを識別するハンドルを使用して](using-a-handle-to-a-registry-key-object.md)します。

次のコード サンプルでは、使用方法を示します**IoOpenDeviceRegistryKey**と**ZwSetValueKey**デバイスのハードウェア キーの下に"Value"をという名前の値に関連付けられているデータを設定します。

```cpp
PDEVICE_OBJECT pDeviceObject; // A pointer to the PDO for the device.
HANDLE handle;
UNICODE_STRING ValueName;
ULONG Value = 109; // This is the value we're setting the key to.
NTSTATUS status;

RtlInitUnicodeString(&ValueName, L"Value");

status = IoOpenDeviceRegistryKey(pDeviceObject, PLUGPLAY_REGKEY_DEVICE, KEY_READ, &handle);

if (NTSUCCESS(status)) {
  status = ZwSetValueKey(handle, ValueName, 0, REG_DWORD, &Value, sizeof(ULONG));
  if (NTSUCCESS(status) {
    ZwClose(handle);
  } else {
    // Handle error.
  }
  // Handle error.
}
```

レジストリ キーへのアクセスを制限できることに注意してくださいそのため、への呼び出し[ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)と[ **IoOpenDeviceInterfaceRegistryKey** 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)ために必要な最低限の権限を指定する必要があります*DesiredAccess*します。 要求した場合、ドライバーへのアクセス権限が許可されていません、いずれかのルーチンがステータスを返します\_アクセス\_が拒否されました。 具体的には、ドライバーがキーを指定する必要があります\_すべて\_アクセスします。

 

 




