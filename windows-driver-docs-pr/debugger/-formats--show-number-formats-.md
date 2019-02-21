---
title: .formats (数値の形式を表示する)
description: .Formats コマンドは、現在のスレッドとプロセスのコンテキスト内のシンボルまたは式を評価し、複数の数値形式で表示されます。
ms.assetid: 9eac92b3-5137-4adb-a074-31510dc9bff7
keywords:
- .formats (数値の形式を表示する) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .formats (Show Number Formats)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 11a836c5c1dca791b17d16c5bee08f0e1e0dc5dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558221"
---
# <a name="formats-show-number-formats"></a>.formats (数値の形式を表示する)


**.Formats**コマンドは、現在のスレッドとプロセスのコンテキスト内のシンボルまたは式を評価し、複数の数値形式で表示されます。

```dbgcmd
.formats expression 
```

## <a name="span-idddkmetashownumberformatsdbgspanspan-idddkmetashownumberformatsdbgspanparameters"></a><span id="ddk_meta_show_number_formats_dbg"></span><span id="DDK_META_SHOW_NUMBER_FORMATS_DBG"></span>パラメーター


<span id="_______expression______"></span><span id="_______EXPRESSION______"></span> *expression*   
評価する式を指定します。 構文の詳細については、次を参照してください。[数値式の構文](numerical-expression-syntax.md)します。

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

単精度と倍精度浮動小数点形式と同様に、16 進数、10 進、8 進数、およびバイナリ形式では、式の評価結果が表示されます。 ASCII 文字の形式は、バイトは、対応する標準の ASCII 文字とも表示されます。 式は、許容範囲内にある場合にもタイムスタンプとして解釈されます。

次の例は、 **.formats**コマンド。

```dbgcmd
0:000> .formats 1c407e62
Evaluate expression:
  Hex:     1c407e62
  Decimal: 473988706
  Octal:   03420077142
  Binary:  00011100 01000000 01111110 01100010
  Chars:   .@~b
  Time:    Mon Jan 07 15:31:46 1985
  Float:   low 6.36908e-022 high 0
  Double:  2.34182e-315
```

**時間**フィールドが CRT タイムスタンプの形式で、32 ビット値を表示し、FILETIME 形式の 64 ビット値を表示します。 FILETIME 形式には、(ミリ秒) が含まれています。 とは CRT の形式であるために、これらの形式を区別できます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**?(式の評価)**](---evaluate-expression-.md)

[**??(C++ の式の評価)**](----evaluate-c---expression-.md)

 

 






