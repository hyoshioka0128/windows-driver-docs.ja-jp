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
ms.openlocfilehash: ffa464523400ac527775ae1a350c74a45749e4cb
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350389"
---
# <a name="plug-and-play-registry-routines"></a>プラグ アンド プレイ レジストリ ルーチン


プラグ アンド プレイ マネージャーは、ドライバー、そのデバイス、およびそのデバイス インターフェイスのインスタンスを特定のレジストリ キーを関連付けます。 ドライバーは、これらのキーを使用して、ドライバー、または特定のデバイスまたはデバイス インターフェイスのインスタンスに関連付けられた永続的なプロパティを格納できます。

ドライバーは、これらのキーを直接アクセスする必要があることはありません。 Windows の将来のバージョン可能性があります、または情報を格納別の場所にレジストリで、レジストリ外全体。 ドライバーは、次のツリー内のすべてのキーを直接アクセスできないする必要があります。

-   HKLM\\システム\\CurrentControlSet\\コントロール\\クラス

-   HKLM\\システム\\CurrentControlSet\\コントロール\\DeviceClasses

-   HKLM\\システム\\CurrentControlSet\\列挙型

-   HKLM\\システム\\CurrentControlSet\\ハードウェア プロファイル

代わりに、ドライバーを使用して、 [ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)と[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)ルーチンの PnP にアクセスするにはキー。

PnP マネージャーでは、ドライバーの場合、ドライバーのソフトウェアのキー、および各デバイスの場合、デバイスのハードウェア キーと呼ばれるキーと呼ばれる 1 つのキーを割り当てます。 **IoOpenDeviceRegistryKey**ルーチンがいずれかのキーを開くことができます。 値、 *DevInstKeyType*を開くには、どのキーを指定します。 PLUGPLAY を指定\_REGKEY\_ドライバー、ソフトウェア キーまたは PLUGPLAY を開く\_REGKEY\_ハードウェア キーへのデバイス。 *デバイス オブジェクト*パラメーターは、デバイスまたはドライバーを指定します。 (ドライバーは、and 演算 PLUGPLAY によって、現在のハードウェア プロファイルを基準とそのハードウェアとソフトウェア キーにもアクセスできます\_REGKEY\_現在\_に HWPROFILE *DevInstKeyType*)。

**IoOpenDeviceInterfaceRegistryKey**特定のデバイス インターフェイスのインスタンスに関連付けられたキーを開きます。 これは、その名前で、インスタンスが識別される、 [ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)によって返される[ **IoGetDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff549186)、[ **IoGetDeviceInterfaceAlias**](https://msdn.microsoft.com/library/windows/hardware/ff549180)、または[ **IoRegisterDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff549506)します。 として文字列が渡される、 *SymbolicLinkValue*パラメーターを**IoOpenDeviceInterfaceRegistryKey**します。

INF ファイル、またはを使用して、これらのキーを設定することも、 **SetupDi * Xxx*** ルーチン。 詳細については、[ドライバーのレジストリ キー](https://msdn.microsoft.com/library/windows/hardware/ff549538)を参照してください。

両方[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)と[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)としてアクセス権を持つ、開いているキー ハンドルを提供指定された、 *DesiredAccess*パラメーター。 ドライバーを使用して、その後、 **Zw * Xxx*** レジストリのルーチンなど[ **ZwQueryValueKey** ](https://msdn.microsoft.com/library/windows/hardware/ff567069)と[ **ZwSetValueKey**](https://msdn.microsoft.com/library/windows/hardware/ff567109)にアクセスして、キーを操作します。 ドライバーが呼び出すことによって、ハンドルを閉じ、ドライバーは不要になったハンドルを使用して後、 [ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)します。 詳細については、[レジストリ キー オブジェクトを識別するハンドルを使用して](using-a-handle-to-a-registry-key-object.md)を参照してください。

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

レジストリ キーへのアクセスを制限できることに注意してくださいそのため、への呼び出し[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)と[ **IoOpenDeviceInterfaceRegistryKey** 。](https://msdn.microsoft.com/library/windows/hardware/ff549433)ために必要な最低限の権限を指定する必要があります*DesiredAccess*します。 要求した場合、ドライバーへのアクセス権限が許可されていません、いずれかのルーチンがステータスを返します\_アクセス\_が拒否されました。 具体的には、ドライバーがキーを指定する必要があります\_すべて\_アクセスします。

 

 




