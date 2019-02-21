---
title: .scriptload (スクリプトの読み込み)
description: .Scriptload コマンドは読み込むし、指定したスクリプト ファイルを実行します。
ms.assetid: 1D4C9587-1491-4D34-9D09-45587B272641
keywords:
- .scriptload (スクリプトの読み込み) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptload (Load Script)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77bd18d5268a62cb7ca21bd99b47c0b63a05a560
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537003"
---
# <a name="scriptload-load-script"></a>.scriptload (スクリプトの読み込み)


**.Scriptload**コマンドは読み込み、指定したスクリプト ファイルを実行します。

```dbgcmd
.scriptload ScriptFile
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______ScriptFile______"></span><span id="_______scriptfile______"></span><span id="_______SCRIPTFILE______"></span> *ScriptFile*   
読み込むスクリプト ファイルの名前を指定します。 *ScriptFile* .js ファイル名拡張子を含める必要があります。 絶対または相対パスを使用できます。 相対パスで、デバッガーを起動しているディレクトリに対して相対的な。 空白を含むファイル パスがサポートされていません。

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

.Scriptload コマンドはスクリプトを読み込むし、スクリプトを実行します。 次のコマンドは、TestScript.js の読み込みが成功したを示しています。

```dbgcmd
0:000> .scriptload C:\WinDbg\Scripts\TestScript.js
JavaScript script successfully loaded from 'C:\WinDbg\Scripts\TestScript.js'
```

初期読み込みと、スクリプトの実行でエラーがある場合、エラーが表示されますコンソールでは、行の数とエラー メッセージにします。

```dbgcmd
0:000:x86> .scriptload C:\WinDbg\Scripts\TestScript.js
0:000> "C:\WinDbg\Scripts\TestScript.js" (line 11 (@ 1)): Error (0x80004005): Syntax error
Error: Unable to execute JavaScript script 'C:\WinDbg\Scripts\TestScript.js'
```

.Scriptload コマンドは、JavaScript で、次が実行されます。

-   ルートのコード
-   intializeScript 関数 (存在する場合、スクリプトで)

実行 .scriptload コマンド intializeScript 関数やスクリプトのルート コードを使用して、スクリプトが読み込まれるときに、デバッガー (dx デバッガー) のルート名前空間には、スクリプト内に存在する名前がブリッジされるされ、スクリプトは常に常駐しています。メモリがアンロードされるまで、そのオブジェクトに対するすべての参照が解放されます。

スクリプトは、新しい機能を提供できる、デバッガーの式エバリュエーターでは、デバッガーでのオブジェクト モデルを変更または同様の NatVis ビジュアライザーはほとんどのビジュアライザーとして動作できます。 NavVis とデバッガーの詳細については、次を参照してください。 [ **dx (表示 NatVis 式)**](dx--display-visualizer-variables-.md)します。

JavaScript での操作の詳細については、次を参照してください。 [JavaScript デバッガー Scripting](javascript-debugger-scripting.md)します。 デバッガー オブジェクトに関する詳細については、次を参照してください。 [JavaScript 拡張機能のネイティブ オブジェクト](native-objects-in-javascript-extensions.md)します。

**要件**

.Script コマンドのいずれかを使用するのには、スクリプトのプロバイダーが読み込まれる必要があります。 使用して、 [ **.load (拡張 DLL の読み込み)** ](-load---loadby--load-extension-dll-.md) JavaScript プロバイダを読み込むコマンド。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**.scriptunload (アンロード スクリプト)**](-scriptunload--unload-script-.md)

[Scripting JavaScript デバッガー](javascript-debugger-scripting.md)

 

 






