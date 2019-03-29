---
title: .holdmem (メモリの保持と比較)
description: .Holdmem コマンドでは、メモリ範囲を保存し、その他のメモリの範囲と比較しました。
ms.assetid: d8caa0df-c87d-4378-9a39-cc04760ca0db
keywords:
- 保持し、メモリ (.holdmem) コマンドの比較
- メモリ、保持およびメモリ (.holdmem) コマンドの比較
- .holdmem (保留および比較メモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .holdmem (Hold and Compare Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ffc93cde2e93e7781b494d6d9768b4869b4d4394
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571463"
---
# <a name="holdmem-hold-and-compare-memory"></a>.holdmem (メモリの保持と比較)


**.Holdmem**コマンドは、メモリ範囲を保存しに他のメモリ範囲を比較します。

```dbgcmd
.holdmem -a Range 
.holdmem -d { Range | Address } 
.holdmem -D 
.holdmem -o 
.holdmem -c Range 
```

## <a name="span-idddkmetaholdandcomparememorydbgspanspan-idddkmetaholdandcomparememorydbgspanparameters"></a><span id="ddk_meta_hold_and_compare_memory_dbg"></span><span id="DDK_META_HOLD_AND_COMPARE_MEMORY_DBG"></span>パラメーター


<span id="_______-a_Range_____________"></span><span id="_______-a_range_____________"></span><span id="_______-A_RANGE_____________"></span> **-** **** *範囲*   
保存するメモリの範囲を指定します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______-d___Range___Address__"></span><span id="_______-d___range___address__"></span><span id="_______-D___RANGE___ADDRESS__"></span> **-d** **** { *Range* | *Address* }  
削除するメモリの範囲を指定します。 指定した場合*アドレス*デバッガーがそのアドレスを含む保存済みの範囲を削除します。 指定した場合*範囲*、デバッガーと重複する保存済みの範囲を削除します*範囲*します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______-D______"></span><span id="_______-d______"></span> **-D**   
すべての保存されたメモリ範囲を削除します。

<span id="_______-o______"></span><span id="_______-O______"></span> **-o**   
すべての保存されたメモリ範囲を表示します。

<span id="_______-c_______Range______"></span><span id="_______-c_______range______"></span><span id="_______-C_______RANGE______"></span> **-c** *範囲*   
すべての保存されたメモリ範囲を指定した範囲を比較します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

メモリおよびその他のメモリに関連するコマンドの説明を操作する方法の詳細については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>コメント
-------

**.Holdmem**コマンドは、メモリ範囲のバイトを比較します。

指定されたメモリの場所のいずれかの仮想アドレス空間に存在しない、コマンドはエラーを返します。

 

 





