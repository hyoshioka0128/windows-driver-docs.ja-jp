---
title: .fnent (関数のデータを表示)
description: .Fnent コマンドには、指定された関数の関数のテーブルのエントリに関する情報が表示されます。
ms.assetid: 914caf55-2fbf-4f30-af6e-e666dc47c7da
keywords:
- 関数のデータ (.fnent) コマンドが表示されます。
- .fnent (関数のデータを表示) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fnent (Display Function Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22385219eaa6914c6561e6ce3acf0d6186d8075b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529660"
---
# <a name="fnent-display-function-data"></a>.fnent (関数のデータを表示)


**.Fnent**コマンドが、指定された関数の関数のテーブルのエントリに関する情報を表示します。

```dbgcmd
.fnent Address
```

## <a name="span-idddkmetadisplayfunctiondatadbgspanspan-idddkmetadisplayfunctiondatadbgspanparameters"></a><span id="ddk_meta_display_function_data_dbg"></span><span id="DDK_META_DISPLAY_FUNCTION_DATA_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
関数のアドレスを指定します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

シンボルの検索アルゴリズム、 **.fnent**コマンドは、の場合と同じ、 [ **ln (最も近いシンボルの一覧)** ](ln--list-nearest-symbols-.md)コマンド。 まず、表示には、最も近いシンボルが表示されます。 次に、デバッガーでは、これらのシンボルの最初の関数のエントリが表示されます。

関数のテーブルに最も近いシンボルがない場合は、情報は表示されません。

次の例では、可能な表示を示します。

```dbgcmd
0:001> .fnent 77f9f9e7
Debugger function entry 00b61f50 for:
(77f9f9e7)   ntdll!RtlpBreakWithStatusInstruction   |  (77f9fa98)   ntdll!DbgPrintReturnControlC

Params:    1
Locals:    0
Registers: 0

0:001> .fnent 77f9fa98
Debugger function entry 00b61f70 for:
(77f9fa98)   ntdll!DbgPrintReturnControlC   |  (77f9fb21)   ntdll!DbgPrompt

Non-FPO

0:001> .fnent 01005a60
No function entry for 01005a60
```

 

 





