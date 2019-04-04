---
title: n (基底数の設定)
description: N コマンドは、既定数基本 (小数点) を指定した値に設定または基本の現在の数が表示されます。このコマンドを混同しないでください、~ (スレッドの中断) n コマンド。
ms.assetid: a2af7cf4-b0f1-4ceb-b9c0-7517a9517c3e
keywords:
- n (セット数ベース) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- n (Set Number Base)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c2c1e5e9c10adff45a1d86c6aaf55a69096676a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577782"
---
# <a name="n-set-number-base"></a>n (基底数の設定)


**N**コマンド (基数)、既定数を基本を指定した値に設定または基本の現在の数が表示されます。

このコマンドを混同しないでください、 [ **~ (スレッドの中断) n** ](-n--suspend-thread-.md)コマンド。

```dbgcmd
n [Radix]
```

## <a name="span-idddkcmdsetnumberbasedbgspanspan-idddkcmdsetnumberbasedbgspanparameters"></a><span id="ddk_cmd_set_number_base_dbg"></span><span id="DDK_CMD_SET_NUMBER_BASE_DBG"></span>パラメーター


<span id="_______Radix______"></span><span id="_______radix______"></span><span id="_______RADIX______"></span> *基数*   
数値の表示とエントリに使用される基本既定数を指定します。 次の値のいずれかを使用することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[値]</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>8 進数</p></td>
</tr>
<tr class="even">
<td align="left"><p>10</p></td>
<td align="left"><p>10 進数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>16</p></td>
<td align="left"><p>16 進数</p></td>
</tr>
</tbody>
</table>

 

省略した場合*基数*基数、現在の既定値が表示されます。

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

 

<a name="remarks"></a>コメント
-------

現在の基数は、入力と出力の MASM 式に影響します。 入力または C++ の式の出力は影響しません。 これらの式の詳細については、[を評価する式](evaluating-expressions.md)を参照してください。

デバッガーが開始されると、既定の基数は 16 に設定します。

すべての MASM 式では、数値は (16、10、または 8) は、現在の基数での数値として解釈されます。 既定の基数を指定して上書きできます、 **0 x**プレフィックス (16 進数)、 **0n**プレフィックス (10 進数)、 **0t**プレフィックス (8 進数)、または**0y**プレフィックス (バイナリ)。

 

 





