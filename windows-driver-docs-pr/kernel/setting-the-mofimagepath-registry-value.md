---
title: MofImagePath レジストリ値の設定
description: MofImagePath レジストリ値の設定
ms.assetid: b8c43cd3-d4f4-4f1e-b692-8005d845d64a
keywords:
- WMI の WDK カーネルでは、スキーマの公開
- 発行の WMI スキーマ WDK
- 発行 WDK WMI スキーマ
- MOF ファイルの WDK WMI
- MofImagePath
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bb76d227a5bb056d0afab1d092ad614b7cea909
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385853"
---
# <a name="setting-the-mofimagepath-registry-value"></a>MofImagePath レジストリ値の設定





コンパイル済みの MOF リソースを含め、DLL などの別のファイルに設定することによって、ドライバーのスキーマを公開できます**MofImagePath**レジストリにそのファイルのパス。 この方法で公開されるスキーマは、ドライバーを再コンパイルしなくても更新できます。

別のファイルにドライバーのスキーマを発行します。

1.  」の説明に従って、MOF ファイルをコンパイル[ドライバーの MOF ファイルをコンパイルする](compiling-a-driver-s-mof-file.md)します。

2.  リソースの DLL などのファイルとしてコンパイル済みの MOF ファイルを含めます。

3.  追加、 **MofImagePath**ドライバーのサービス キーの下のレジストリ値。 たとえば、という名前のドライバーのレジストリ値を次に示します*DriverName*:

    ```cpp
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services
        \DriverName
            MofImagePath    "\SystemRoot\System32\Drivers\DriverNameMof.dll"
    ```

このキーは、次のように、ドライバーの INF ファイルで設定できます。

```cpp
; This is the Services section for the driver
[Driver_service_install_section]
AddReg=Driver_AddReg

; This is the Services AddReg section declared above.
[Driver_AddReg]
HKR,,MofImagePath,,DriverMof.dll 
```

参照してください[ **INF DDInstall.Services セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)と[ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)詳細についてはします。

 

 




