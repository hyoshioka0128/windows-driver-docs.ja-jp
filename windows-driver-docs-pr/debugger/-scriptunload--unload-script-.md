---
title: .scriptunload (スクリプトのアンロード)
description: .Scriptunload コマンドでは、指定されたスクリプトをアンロードします。
ms.assetid: 015703C2-31E2-46B4-8F89-1EA52DB7E6FC
keywords:
- .scriptunload (アンロード スクリプト) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptunload (Unload Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6968ad77c18353f619432b2c7fc85256c9c02995
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330842"
---
# <a name="scriptunload-unload-script"></a>.scriptunload (スクリプトのアンロード)


**.Scriptunload**コマンドは、指定したスクリプトをアンロードします。

```dbgcmd
.scriptunload ScriptFile
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span> *ScriptFile*   
アンロードするスクリプト ファイルの名前を指定します。 *ScriptFile* .js ファイル名拡張子を含める必要があります。 絶対または相対パスを使用できます。 相対パスで、デバッガーを起動しているディレクトリに対して相対的な。 空白を含むファイル パスがサポートされていません。

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

.Scriptunload コマンドでは、読み込まれたスクリプトをアンロードします。 次のコマンド構文を使用して、スクリプトをアンロードするには

```dbgcmd
0:000:x86> .scriptunload C:\WinDbg\Scripts\TestScript.js
JavaScript script unloaded from 'C:\WinDbg\Scripts\TestScript.js'
```

スクリプト内のオブジェクトに未解決の参照がある場合は、スクリプトの内容がリンクされますが、スクリプトは、このようなすべての参照が解放されるまでメモリに残る可能性があります。

JavaScript での操作の詳細については、次を参照してください。 [JavaScript デバッガー Scripting](javascript-debugger-scripting.md)します。 デバッガー オブジェクトに関する詳細については、次を参照してください。 [JavaScript 拡張機能のネイティブ オブジェクト](native-objects-in-javascript-extensions.md)します。

**必要条件**

.Script コマンドのいずれかを使用するのには、スクリプトのプロバイダーが読み込まれる必要があります。 使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダー dll を読み込むコマンド。

```dbgcmd
0:000> .load C:\ScriptProviders\jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**.scriptload (スクリプトの読み込み)**](-scriptload--load-script-.md)

[JavaScript デバッガー スクリプト](javascript-debugger-scripting.md)

 

 






