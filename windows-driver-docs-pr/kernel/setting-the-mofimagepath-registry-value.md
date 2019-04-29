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
ms.openlocfilehash: 0a8f020e3d1cadaa02f5a7e4a2c3213482b0ac90
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385496"
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

参照してください[ **INF DDInstall.Services セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547349)と[ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)詳細についてはします。

 

 




