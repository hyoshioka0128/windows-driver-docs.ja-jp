---
title: MS-DOS デバイス名の概要
description: MS-DOS デバイス名の概要
ms.assetid: 44b2f871-56e1-46d3-aab4-c38f498d089d
keywords:
- MS-DOS デバイス名 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83fac0d285bcaaf5749287f7c0e387b503bf0302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838625"
---
# <a name="introduction-to-ms-dos-device-names"></a>MS-DOS デバイス名の概要





非 WDM ドライバーによって作成される名前付きデバイスオブジェクトには、通常、MS-DOS デバイス名があります。 MS-DOS デバイス名は、オブジェクトマネージャーのシンボリックリンクであり、 **\\DosDevices\\** <em>dosdevices</em>の形式で名前が付けられています。

MS-DOS デバイス名を持つデバイスの例として、シリアルポート COM1 があります。 これには、MS-DOS デバイス名 **\\DosDevices\\COM1**があります。 同様に、C ドライブには **\\DosDevices\\c:** という名前が付いています。

通常、WDM ドライバーは、デバイスの MS-DOS デバイス名を提供しません。 代わりに、WDM ドライバーは、 [**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)ルーチンを使用してデバイスインターフェイスを登録します。 デバイスインターフェイスでは、特定の名前付け規則ではなく、デバイスの機能によってデバイスが指定されます。 詳細については、「[デバイスインターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)」を参照してください。

ドライバーは、ユーザーモードプログラムを操作するためにデバイスが特定の既知の MS-DOS デバイス名を持っている必要がある場合にのみ、MS-DOS デバイス名を指定する必要があります。

ドライバーは、Ioてデバイスへのシンボリックリンクを作成するために、 [**ioて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink)デバイスオブジェクトの MS-DOS デバイス名を提供します。 たとえば、次のコード例では、 **\\DosDevices\\** <em>dosdevices</em>から **\\デバイス\\** <em>DeviceName</em>にシンボリックリンクを作成します。

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

システムでは、 **\\DosDevices**ディレクトリの複数のバージョンがサポートされていることに注意してください。 意図したバージョンのシンボリックリンクがドライバーによって作成されていることを確認します。 詳細については、「[ローカルおよびグローバルの MS-DOS デバイス名](local-and-global-ms-dos-device-names.md)」を参照してください。

**Dosdevices**名前空間にユーザーモードでアクセスするには\\\\を指定します。ファイル名を開いたときに **\\します。** **CreateFile ()** を呼び出すことによって、対応するデバイスをユーザーモードで開くことができます。

たとえば、次のコード例では、\\\\DosDevices\\\\*Dosdevices*デバイスをユーザーモードで開きます。

```cpp
file = CreateFileW(L"\\\\.\\DosDeviceName",
  GENERIC READ | GENERIC WRITE,
    0,
    NULL,
    OPEN_EXISTING,
    0,
    NULL);
```

ユーザーモードの**デバイス**ルーチンを使用して、ユーザーモードアプリケーションからシンボリックリンクを作成することもできます。 詳細については、Microsoft Windows SDK を参照してください。

 

 




