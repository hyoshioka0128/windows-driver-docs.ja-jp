---
title: Reg2inf
description: Reg2inf は、ドライバー パッケージをユニバーサルにするレジストリ キーに変換するツールです。
ms.assetid: e43a137e-c08a-4715-84f7-32cda67399e3
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 788a4a0288461f79e1f26a1ea3a128f643bd5e32
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356388"
---
# <a name="reg2inf"></a>Reg2inf
 
ドライバー パッケージ INF レジストリ変換ツール (`reg2inf.exe`) ツールは、レジストリ キーとその値、または実装する COM .dll に変換します、 [ **DllRegisterServer** ](https://docs.microsoft.com/windows/desktop/api/olectl/nf-olectl-dllregisterserver)を一連の定期的な[。INF AddReg ディレクティブ](../install/inf-addreg-directive.md)ドライバー パッケージ INF ファイルに組み込むことです。  このツールは、既存の変換する際に特に役立ちます[INF RegisterDlls ディレクティブ](../install/inf-registerdlls-directive.md)ように、INF ファイル ユニバーサル INF AddReg ディレクティブにします。  ユニバーサル INF ファイルに関する詳細については、次を参照してください。[ユニバーサル INF ファイルを使用して](../install/using-a-universal-inf-file.md)します。
 
このツールは Windows 10 バージョン 1709 以降、WDK 10 のインストールの一部として同梱されています。 検索、これを WDK 10 のインストールの \tools サブディレクトリにたとえば`c:\Program Files(x86)\Windows Kits\10\tools\`します。 

Reg2inf が COM 登録を生成しようとすると、COM 登録を提供する完全なレジストリ状態が取り込みません可能性があります。 いつものように、完全性と正確性、ツールの出力を検査し、結果をテストしてください。 

## <a name="running-reg2inf-from-the-command-line"></a>コマンドラインから実行中の Reg2inf 
 
このセクションでは、Reg2inf のコマンド ライン オプションを示します。

```
USAGE: reg2inf.exe [/key <path> | /dll <filename>] [/targetkey <path>]

/key <registry key path>
    Process a specific registry key, e.g.: reg2inf /key HKEY_LOCAL_MACHINE\SOFTWARE\Fabrikam
/dll <module filename>
    Process a COM DLL module that implements DllRegisterServer entrypoint, typically called by regsvr32 or legacy INF RegisterDlls directive in order to register COM class under HKEY_CLASSES_ROOT, e.g.: reg2inf /dll %SystemRoot%\System32\fabkobj.dll
/targetkey <registry key path>
    Remap target registry key to be under a different base key path, e.g.: reg2inf /key HKLM\SYSTEM\Temp /targetkey HKR\Parameters
```

**注**Reg2inf では、完全なパスの長さが 259 文字を超えないことが必要です。 
