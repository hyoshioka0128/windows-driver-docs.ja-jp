---
title: .extpath (拡張機能のパスの設定)
description: .Extpath コマンドでは、拡張 DLL の検索パスを設定または表示することができます。
ms.assetid: 957028ff-d8f4-41ab-bdaa-ff1bbe886bec
keywords:
- .extpath (拡張機能パスの設定) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .extpath (Set Extension Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10fe37d68e0240461f34f5ba75b3ce145b4a9ccc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334485"
---
# <a name="extpath-set-extension-path"></a>.extpath (拡張機能のパスの設定)


**.Extpath**コマンドを設定または拡張機能の DLL 検索パスが表示されます。

```dbgcmd
.extpath[+] [Directory[;...]]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="______________"></span> +   
デバッガーが (パスを置き換えて) ではなく以前の拡張 DLL 検索パスに新しいディレクトリを追加することを示します。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *ディレクトリ*   
検索パスに配置する 1 つまたは複数のディレクトリを指定します。 指定しない場合*ディレクトリ*、現在のパスが表示されます。 複数のディレクトリをセミコロンで区切ることができます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

拡張 Dll の読み込みと拡張機能の検索パスの詳細については、次を参照してください。[デバッガー拡張 Dll の読み込み](loading-debugger-extension-dlls.md)します。

<a name="remarks"></a>コメント
-------

拡張 DLL の検索パスは、各デバッグ セッションの開始時に、その既定値にリセットされます。

ライブ カーネル モードのデバッグ中にターゲット コンピューターの再起動を結果の新しいデバッグ セッションを開始します。 拡張 DLL に対して行った変更を検索できるように、カーネル モードのデバッグ中にパスはターゲット コンピューターの再起動の間で保持されません。

拡張 DLL の検索パスの既定値には、デバッガーを既知のすべての拡張機能のパスとパス環境変数内のすべてのパスが含まれています。 たとえば、%%path 環境変数の値を持つ`C:\Windows\system32;C:\Windows`します。 DLL の拡張機能の検索パスの既定値は次のようになります。

```dbgcmd
0:000> .extpath
Extension search path is: C:\Program Files\Debugging Tools for Windows (x64)\WINXP;C:\Program Files\
Debugging Tools for Windows (x64)\winext;C:\Program Files\Debugging Tools for Windows (x64)\winext\
arcade;C:\Program Files\Debugging Tools for Windows (x64);C:\Program Files\Debugging Tools for 
Windows (x64)\winext\arcade;C:\Windows\system32;C:\Windows
```

 

 





