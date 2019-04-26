---
title: ks.graph
description: Ks.graph 拡張機能のコマンドは、位相的に並べ替えられた順序で、カーネル モードのグラフの説明テキストを表示します。
ms.assetid: b9725499-9db3-422f-850b-97db4865b74d
keywords:
- デバッグ ks.graph Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ks.graph
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 468efe03adea8c5d2309cb1fc778c4989304030e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336243"
---
# <a name="ksgraph"></a>!ks.graph


**! Ks.graph**拡張機能のコマンドは、位相的に並べ替えられた順序で、カーネル モードのグラフの説明テキストを表示します。

```dbgcmd
!ks.graph Object [Level] [Flags] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Object______"></span><span id="_______object______"></span><span id="_______OBJECT______"></span> *オブジェクト*   
グラフの開始点として使用するオブジェクトへのポインターを指定します。 次のいずれかへのポインターである必要があります: ファイル オブジェクト、IRP、pin、またはフィルター。

<span id="_______Level______"></span><span id="_______level______"></span><span id="_______LEVEL______"></span> *レベル*   
(省略可能)。 0 ~ 7 で表示する詳細のレベルを指定の値を大きく表示徐々 に詳細なスケールします。 使用可能なすべての詳細を表示するには、7 の値を指定します。 レベルは、 **! ks.graph**のものと同じ[ **! ks.dump**](-ks-dump.md)します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
任意。 表示される情報の種類を指定します。 *フラグ*次のビットの組み合わせにすることができます。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
Irp の一覧を表示では、グラフ内の各暗証番号 (pin) インスタンスにキューに登録します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
保留になっている Irp の一覧を表示、グラフ内の各暗証番号 (pin) インスタンスから。 待機している、暗証番号 (pin) を認識している Irp のみが表示されます。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
問題のあるフィルターの停止しているグラフを分析します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>winxp\Ks.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Ks.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。[ストリーミングのカーネル デバッグ](kernel-streaming-debugging.md)します。

<a name="remarks"></a>コメント
-------

このコマンドは、大量の処理に時間をかかる場合があります。

問題を **! ks.graph**ヘルプの引数なしでコマンド。

次の例に示します、 **! ks.graph**フィルター オブジェクトのアドレスを表示する。

```dbgcmd
kd> !graph 829493c4
Attempting a graph build on 829493c4...  Please be patient...

Graph With Starting Point 829493c4:

"avssamp" Filter 82949350, Child Factories 1
    Output Factory 0 [Video/General Capture]:
        Pin 8293f4f0 (File 82503498) Irps(q/p) = 2, 0
```

 

 





