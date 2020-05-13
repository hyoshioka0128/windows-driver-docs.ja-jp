---
title: Reg2inf
description: Reg2inf は、ドライバーパッケージを universal にするためにレジストリキーを変換するツールです。
ms.assetid: e43a137e-c08a-4715-84f7-32cda67399e3
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: b815eff7e077562b89c237bdacbb756ec6f50c23
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83235287"
---
# <a name="reg2inf"></a>Reg2inf
 
ドライバーパッケージ INF レジストリ変換ツール ( `reg2inf.exe` ) ツールは、 [**DllRegisterServer**](https://docs.microsoft.com/windows/desktop/api/olectl/nf-olectl-dllregisterserver)ルーチンを実装するレジストリキーとその値または COM .dll を、ドライバーパッケージの inf ファイルに含めるための一連の[INF AddReg ディレクティブ](../install/inf-addreg-directive.md)に変換します。  このツールは、INF ファイルをユニバーサルにするために、既存の[Inf RegisterDlls ディレクティブ](../install/inf-registerdlls-directive.md)を inf AddReg ディレクティブに変換する場合に特に便利です。  ユニバーサル INF ファイルの詳細については、「 [UNIVERSAL Inf ファイルの使用](../install/using-a-universal-inf-file.md)」を参照してください。
 
Windows 10 バージョン1709以降、ツールは WDK 10 インストールの一部として出荷されます。 これは、たとえば、WDK 10 インストールの \ tools サブディレクトリに `c:\Program Files(x86)\Windows Kits\10\tools\` あります。 

Reg2inf は COM 登録の生成を試みますが、COM 登録によって提供される完全なレジストリ状態をキャプチャすることはできません。 常に、ツールの出力で完全性と正確性を検査し、結果をテストする必要があります。 

## <a name="running-reg2inf-from-the-command-line"></a>コマンドラインからの Reg2inf の実行 
 
このセクションでは、Reg2inf のコマンドラインオプションの一覧を示します。

```
USAGE: reg2inf.exe [/key <path> | /dll <filename>] [/targetkey <path>]

/key <registry key path>
    Process a specific registry key, e.g.: reg2inf /key HKEY_LOCAL_MACHINE\SOFTWARE\Fabrikam
/dll <module filename>
    Process a COM DLL module that implements DllRegisterServer entrypoint, typically called by regsvr32 or legacy INF RegisterDlls directive in order to register COM class under HKEY_CLASSES_ROOT, e.g.: reg2inf /dll %SystemRoot%\System32\fabkobj.dll
/targetkey <registry key path>
    Remap target registry key to be under a different base key path, e.g.: reg2inf /key HKLM\SYSTEM\Temp /targetkey HKR\Parameters
```

**メモ**Reg2inf では、完全パスの長さが259文字を超えないようにする必要があります。 

## <a name="registering-a-com-component-in-an-inf-file"></a>INF ファイルに COM コンポーネントを登録する

次のスニペットは、Reg2inf によって生成されるように、INF AddReg 構文を使用して単純な COM クラスを登録する方法を示しています。

```cpp
[ComClass_AddReg]
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084},,,"Sample Class"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,,%REG_EXPAND_SZ%,"%13%\comobj.dll"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,ThreadingModel,,"Both"
```

