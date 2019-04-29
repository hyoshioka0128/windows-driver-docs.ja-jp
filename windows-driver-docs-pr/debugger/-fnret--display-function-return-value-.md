---
title: .fnret (関数の戻り値の表示)
description: .Fnret コマンドでは、関数の戻り値に関する情報が表示されます。
ms.assetid: b7ce3047-5b0a-43ba-877f-76235139d66c
keywords:
- .fnret (表示関数の戻り値) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .fnret (Display Function Return Value)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 51eb7e56fb249b72ba9abf3034e54bad3e17230c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336669"
---
# <a name="fnret-display-function-return-value"></a>.fnret (関数の戻り値の表示)


**.Fnret**コマンドは、関数の戻り値に関する情報を表示します。

```dbgcmd
.fnret [/s] Address [Value] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="________s______"></span><span id="________S______"></span> **/s**   
セット、 **$callret**表示されている、型情報を含む戻り値と一致する擬似レジスタ。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
関数のアドレスを指定します。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span> *値*   
表示する戻り値を指定します。 含める場合*値*、 **.fnret**キャスト*値*指定の関数の戻り値の型を戻り値の型の形式で表示します。 省略した場合*値*デバッガーは、戻り値のレジスタから関数の戻り値を取得します。

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

含める場合は、*値*パラメーター、 **.fnret**コマンドは、のみこの値は、適切な型にキャストし、結果を表示します。

省略した場合*値*デバッガーは、この値を決定する戻り値のレジスタを使用します。 関数が、関数よりも最近返された場合、*アドレス*パラメーターを指定します、表示される値はこの関数によって返される値であるいない可能性があります。

 

 





