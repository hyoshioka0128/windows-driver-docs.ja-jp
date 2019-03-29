---
title: コマンド ライン プロンプトから、デバイスのプロパティ ダイアログ ボックスを呼び出す
description: コマンドライン プロンプトからのデバイスのプロパティ ダイアログ ボックスの呼び出し
ms.assetid: 616c93ee-8360-4bab-8e08-48a55cd617f1
keywords:
- デバイスのプロパティ ダイアログ ボックスの WDK デバイスのインストール
- デバイスのプロパティ ダイアログ ボックスを呼び出す
- DeviceProperties_RunDLL WDK デバイスのインストール
- マシンのパラメーター名フィールド WDK デバイスのインストール
- デバイス インスタンス ID パラメーター フィールド WDK デバイス命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00964b69e87ff3846041d34e7d3e6629eb47446e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570089"
---
# <a name="invoking-a-device-properties-dialog-box-from-a-command-line-prompt"></a>コマンドライン プロンプトからのデバイスのプロパティ ダイアログ ボックスの呼び出し


[DeviceProperties_RunDLL](deviceproperties-rundll-function-prototype.md)からコマンド ライン プロンプトを使用して、デバイス マネージャーでの関数を呼び出すことが*rundll32.exe*します。 次のコード例は、呼び出しの形式を示しています。 **DeviceProperties_RunDLL**コマンド プロンプトからです。

```cpp
rundll32.exe devmgr.dll, DeviceProperties_RunDLL machine-name-parameter device-instance-ID-parameter
```

形式と要件、*マシン-名前-パラメーター*フィールドは指定されたコマンドライン文字列の説明と同じ、 *lpCmdLine*パラメーターの**DeviceProperties_RunDLL**します。 形式と要件、*デバイス インスタンス ID パラメーター*フィールドは、の説明と同じではまた、 *lpCmdLine*コマンドライン文字列は、次の追加要件の対象。場合、*デバイス インスタンス ID*サブフィールド含むのアンパサンド (&)、*デバイス インスタンス ID*サブフィールドを引用符 (") で囲む必要があります。

次のコード例では、形式と提供するための要件を示しています、*マシン-名前-パラメーター*と*デバイス インスタンス ID パラメーター*を呼び出す**DeviceProperties_RunDLL。** コマンド ライン プロンプトからです。 これらの例で示した例に対応して[、デバイスのプロパティ ダイアログ ボックス プログラムで、インストール アプリケーションで呼び出す](invoking-a-device-properties-dialog-box-programmatically-in-an-install.md)します。

-   (Windows XP 以降)省略可能な*マシン-名前-パラメーター*フィールドが指定されていないことを示す、既定では、ローカル コンピューターが、コンピューターであります。 必要な*デバイス インスタンス ID パラメーター*装置のフィールド、[デバイス インスタンス識別子](device-instance-ids.md)"ルート\\システム\\0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /DeviceID root\system\0000
    ```

-   (Windows XP 以降)省略可能な*マシン-名前-パラメーター*フィールドが指定されていないことを示す、既定では、ローカル コンピューターが、コンピューターであります。 必要な*デバイス インスタンス ID パラメーター*フィールド デバイス インスタンス id を提供する"PCI\\VEN_8086 & DEV_2445 & SUBSYS_010E1028 REV_12\\3 & 172E68DD & 0 & FD"。 デバイス インスタンス id には、アンパサンドが含まれているため (&)、*デバイス インスタンス ID*サブフィールドは引用符 (") で囲みます。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /DeviceID "PCI\VEN_8086&DEV_2445&SUBSYS_010E1028&REV_12\3&172E68DD&0&FD" 
    ```

-   (Windows 2000 以降)必須*マシン-名前-パラメーター*フィールドが引用符のペアを提供 ("") として*マシン名*コンピューターがローカル コンピューターを示します。 必要な*デバイス インスタンス ID パラメーター*フィールド デバイス インスタンス id を提供する"ルート\\システム\\0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /MachineName "" /DeviceID root\system\0000
    ```

-   (Windows 2000 以降)必要な*マシン-名前-パラメーター*フィールドは、リモート コンピューターの名前を提供"\\\\RemoteMachineAbc"。 必要な*デバイス インスタンス ID パラメーター*フィールド デバイス インスタンス id を提供する"ルート\\システム\\0000"。
    ```cpp
    rundll32.exe devmgr.dll,DeviceProperties_RunDLL /MachineName \\RemoteMachineAbc /DeviceID root\system\0000
    ```

 

 





