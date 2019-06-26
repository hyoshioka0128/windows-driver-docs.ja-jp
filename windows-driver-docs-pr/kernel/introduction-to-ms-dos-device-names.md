---
title: MS-DOS デバイス名の概要
description: MS-DOS デバイス名の概要
ms.assetid: 44b2f871-56e1-46d3-aab4-c38f498d089d
keywords:
- MS-DOS デバイス名の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a61531b6f4004a79e3125b36a578d2ea1eaaf209
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369924"
---
# <a name="introduction-to-ms-dos-device-names"></a>MS-DOS デバイス名の概要





通常、非 WDM ドライバーによって作成される名前付きのデバイス オブジェクトには、MS-DOS のデバイス名があります。 MS-DOS のデバイス名は、フォームの名前を含むオブジェクト マネージャーにシンボリック リンク **\\\dosdevices\z\\** <em>DosDeviceName</em>します。

MS-DOS デバイス名でのデバイスの例では、COM1 シリアル ポートです。 MS-DOS デバイス名が **\\\dosdevices\z\\COM1**します。 C ドライブの名前が同様に、  **\\\dosdevices\z\\c:** します。

WDM ドライバーは、通常は自分のデバイスの MS-DOS デバイス名を指定しません。 WDM ドライバーの代わりに、使用、 [ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)ルーチンをデバイスのインターフェイスを登録します。 デバイスのインターフェイスは、特定の名前付け規則ではなく、それらの機能でデバイスを指定します。 詳細については、次を参照してください。[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)します。

デバイスがユーザー モードのプログラムを使用する特定知ら MS-DOS デバイス名が必要な場合にのみ、MS-DOS デバイス名を指定するには、ドライバーが必要です。

ドライバーを使用してデバイス オブジェクトの MS-DOS デバイス名を提供する、 [ **IoCreateSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatesymboliclink)ルーチンをデバイスへのシンボリック リンクを作成します。 たとえば、次のコード例はからシンボリック リンクを作成します **\\\dosdevices\z\\** <em>DosDeviceName</em>に **\\デバイス\\。**  <em>DeviceName</em>します。

```cpp
UNICODE_STRING DeviceName;
UNICODE_STRING DosDeviceName;
NTSTATUS status;

RtlInitUnicodeString(&DeviceName, L"\\Device\\DeviceName");
RtlInitUnicodeString(&DosDeviceName, L"\\DosDevices\\DosDeviceName");
status = IoCreateSymbolicLink(&DosDeviceName, &DeviceName);
if (!NT_SUCCESS(status)) {
  /* Symbolic link creation failed.  Handle error appropriately. */
}
```

システムの複数のバージョンをサポートしています、  **\\\dosdevices\z**ディレクトリ。 ドライバーが意図されているバージョンでそのシンボリック リンクを作成することを確認します。 詳細については、次を参照してください。[ローカルおよびグローバル MS-DOS デバイス名](local-and-global-ms-dos-device-names.md)します。

アクセスする、 **\dosdevices\z**からユーザー モードでは、名前空間を指定 **\\ \\.\\** ファイル名を開くとします。 呼び出すことによって、ユーザー モードで対応するデバイスを開くことができます**CreateFile()** します。

たとえば、次のコード例が開き、 \\ \\\dosdevices\z\\\\*DosDeviceName*ユーザー モードでのデバイス。

```cpp
file = CreateFileW(L"\\\\.\\DosDeviceName",
  GENERIC READ | GENERIC WRITE,
    0,
    NULL,
    OPEN_EXISTING,
    0,
    NULL);
```

ユーザー モードを使用してシンボリック リンクがユーザー モード アプリケーションから作成することもできます**DefineDosDevice**ルーチン。 詳細については、Microsoft Windows SDK を参照してください。

 

 




