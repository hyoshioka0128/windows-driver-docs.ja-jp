---
title: プラグアンドプレイレジストリルーチン
description: プラグアンドプレイレジストリルーチン
ms.assetid: d526af4e-8b33-46fb-9af9-b0d9b9f1913a
keywords:
- レジストリ WDK カーネル、プラグアンドプレイ
- ドライバーレジストリ情報 WDK カーネル、プラグアンドプレイ
- プラグアンドプレイ WDK カーネル、レジストリルーチン
- ハードウェアキー WDK カーネル
- ソフトウェアキー WDK カーネル
- IoOpenDeviceRegistryKey
- IoOpenDeviceInterfaceRegistryKey
- PnP WDK カーネル、レジストリルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09dc6832584e456d6516a7dd3d884f410fc1ae60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838511"
---
# <a name="plug-and-play-registry-routines"></a>プラグアンドプレイレジストリルーチン


プラグアンドプレイ manager は、特定のレジストリキーをドライバー、そのデバイス、およびデバイスインターフェイスインスタンスに関連付けます。 ドライバーは、これらのキーを使用して、ドライバーに関連付けられている永続的なプロパティや、特定のデバイスまたはデバイスインターフェイスインスタンスを格納できます。

ドライバーは、これらのキーに直接アクセスすることはできません。 将来のバージョンの Windows では、レジストリの別の場所、またはレジストリの外部に情報が保存される場合があります。 ドライバーは、次のツリー内のどのキーにも直接アクセスできないようにする必要があります。

-   HKLM\\SYSTEM\\CurrentControlSet\\Control\\クラス

-   HKLM\\SYSTEM\\CurrentControlSet\\Control\\DeviceClasses 制御

-   HKLM\\システム\\CurrentControlSet\\列挙型

-   HKLM\\SYSTEM\\CurrentControlSet\\ハードウェアプロファイル

代わりに、ドライバーは[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)ルーチンと[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)ルーチンを使用して、PnP キーにアクセスします。

PnP マネージャーは、ドライバーの1つのキー (ドライバーのソフトウェアキー) と、各デバイスのキー (デバイスのハードウェアキーと呼ばれます) を割り当てます。 **IoOpenDeviceRegistryKey**ルーチンを使用して、いずれかのキーを開くことができます。 *Devinstkeytype*パラメーターの値によって、どのキーを開くかが決定されます。 ソフトウェアキーを開くには、PLUGPLAY\_REGKEY\_ドライバーを指定します。または、レジストリ\_デバイスをハードウェアキーに\_します。 *DeviceObject*パラメーターは、デバイスまたはドライバーを指定します。 (また、ドライバーは、現在のハードウェアプロファイルを基準として、現在のハードウェアプロファイルに対して、そのハードウェアとソフトウェアのキーにアクセスすることもできます。これは、PLUGPLAY\_REGKEY\_現在の\_HWPROFILE を*Devinstkeytype*に対して実行すること

**IoOpenDeviceInterfaceRegistryKey**は、特定のデバイスインターフェイスインスタンスに関連付けられているキーを開きます。 インスタンスは、 [**iogetdeviceinterface、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) [**iogetdeviceinterfacealias**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfacealias)、または[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)によって返される[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)である名前で識別されます。 文字列は、 *SymbolicLinkValue*パラメーターとして**IoOpenDeviceInterfaceRegistryKey**に渡されます。

これらのキーは、INF ファイルで設定することも、 **Setupdi * Xxx*** ルーチンを使用して設定することもできます。 詳細については、「[ドライバーのレジストリキー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)」を参照してください。

[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)と[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)はどちらも、 *DesiredAccess*パラメーターで指定されているアクセス権を持つオープンキーハンドルを提供します。 その後、ドライバーは、 [**Zwqueryvaluekey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)や[**Zwqueryvaluekey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)などの**Zw * Xxx*** レジストリルーチンを使用して、キーにアクセスして操作します。 ドライバーがハンドルを使用しなくなった後、ドライバーは[**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出してハンドルを閉じます。 詳細については、「[レジストリキーオブジェクトへのハンドルの使用](using-a-handle-to-a-registry-key-object.md)」を参照してください。

次のコードサンプルでは、 **IoOpenDeviceRegistryKey**と**Zwsetvaluekey**を使用して、デバイスのハードウェアキーの下の "value" という名前の値に関連付けられているデータを設定します。

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

レジストリキーへのアクセスは制限される可能性があるため、 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)と[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)を呼び出す場合は、 *DesiredAccess*に必要な最小限の権限を指定する必要があります。 許可されていないアクセス権をドライバーが要求した場合、どちらのルーチンも、ステータス\_アクセス\_拒否された状態を返します。 特に、ドライバーでは、すべての\_アクセス\_キーを指定しないでください。

 

 




