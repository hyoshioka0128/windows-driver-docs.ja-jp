---
title: .scriptrun (スクリプトの実行)
description: .Scriptrun コマンドは読み込むし、JavaScript を実行します。
ms.assetid: 6481B852-F0B4-4B02-BF7F-81DA21457A40
keywords:
- .scriptrun (スクリプトの実行) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptrun (Run Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 97eeb3313a500ef90130631121f435701206973e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334274"
---
# <a name="scriptrun-run-script"></a>.scriptrun (スクリプトの実行)


.Scriptrun コマンドは読み込むし、JavaScript を実行します。

```dbgcmd
.scriptrun ScriptFile  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span> *ScriptFile*   
読み込みおよび実行するスクリプト ファイルの名前を指定します。 *ScriptFile* .js ファイル名拡張子を含める必要があります。 絶対または相対パスを使用できます。 相対パスで、デバッガーを起動しているディレクトリに対して相対的な。 空白を含むファイル パスがサポートされていません。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

.Scriptrun コマンドはスクリプトを読み込むし、次のコードを実行します。

-   ルート
-   intializeScript
-   invokeScript

コードが読み込まれ、実行時に、確認メッセージが表示されます。

```dbgcmd
0:000> .scriptrun C:\WinDbg\Scripts\helloWorld.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\helloWorld.js'
Hello World!  We are in JavaScript!
```

スクリプトによって行われたすべてのオブジェクト モデル操作は、スクリプトが読み込まれた後または別のコンテンツを再度実行するまで、場所に維持されます。

このテーブルは、どの関数が .scriptload と .scriptrun によって実行されるをまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left"><strong><a href="-scriptload--load-script-.md" data-raw-source="[.scriptload](-scriptload--load-script-.md)">.scriptload</a></strong></td>
<td align="left"><strong>.scriptrun</strong></td>
</tr>
<tr class="even">
<td align="left">ルート</td>
<td align="left">○</td>
<td align="left">○</td>
</tr>
<tr class="odd">
<td align="left">initializeScript</td>
<td align="left">○</td>
<td align="left">○</td>
</tr>
<tr class="even">
<td align="left">invokeScript</td>
<td align="left"></td>
<td align="left">○</td>
</tr>
<tr class="odd">
<td align="left">uninitializeScript</td>
<td align="left"></td>
<td align="left"></td>
</tr>
</tbody>
</table>



このコードを使用すると、コマンドを実行して .script で呼び出される関数を参照してください。

```dbgcmd
// Root of Script
host.diagnostics.debugLog("***>; Code at the very top (root) of the script is always run \n");


function initializeScript()
{
    // Add code here that you want to run every time the script is loaded. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; initializeScript was called \n");
}

function invokeScript()
{
    // Add code here that you want to run every time the script is executed. 
    // We will just send a message to indicate that function was called.
    host.diagnostics.debugLog("***>; invokeScript was called \n");
}
```

JavaScript での操作の詳細については、次を参照してください。 [JavaScript デバッガー Scripting](javascript-debugger-scripting.md)します。 デバッガー オブジェクトに関する詳細については、次を参照してください。 [JavaScript 拡張機能のネイティブ オブジェクト](native-objects-in-javascript-extensions.md)します。

**必要条件**

.Script コマンドのいずれかを使用するのには、スクリプトのプロバイダーが読み込まれる必要があります。 使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダー dll を読み込むコマンド。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**.scriptload (スクリプトの読み込み)**](-scriptload--load-script-.md)

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)










