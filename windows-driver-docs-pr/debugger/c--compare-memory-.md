---
title: c (メモリの比較)
description: C のコマンドは、2 つのメモリ領域に保持されている値を比較します。
ms.assetid: caa02ec3-35d6-4d41-a777-daa264b0dd18
keywords:
- c (比較メモリ) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- c (Compare Memory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1b9710d3b0d13736095086161908cb074088e85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572581"
---
# <a name="c-compare-memory"></a>c (メモリの比較)


**C**コマンドは、2 つのメモリ領域に保持されている値を比較します。

```dbgcmd
c Range Address 
```

## <a name="span-idddkcmdcomparememorydbgspanspan-idddkcmdcomparememorydbgspanparameters"></a><span id="ddk_cmd_compare_memory_dbg"></span><span id="DDK_CMD_COMPARE_MEMORY_DBG"></span>パラメーター


<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span> *範囲*   
比較する 2 つのメモリの範囲の最初。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
比較する 2 つ目のメモリの範囲の開始アドレス。 この範囲のサイズは、最初の範囲に指定したのと同じになります。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

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

その他のメモリに関連するコマンドの説明とメモリの操作の概要については、次を参照してください。[読み取りと書き込みメモリ](reading-and-writing-memory.md)します。

<a name="remarks"></a>コメント
-------

2 つの領域が同一でない場合、デバッガーはいないに同意しない最初の範囲のすべてのメモリ アドレスが表示されます。

たとえば、次のコードを検討してください。

```cpp
void main()
{
    char rgBuf1[100];
    char rgBuf2[100];

    memset(rgBuf1, 0xCC, sizeof(rgBuf1));
    memset(rgBuf2, 0xCC, sizeof(rgBuf2));

    rgBuf1[42] = 0xFF;
}
```

比較する**rgBuf1**と**rgBuf2**、次のコマンドのいずれかを使用します。

```dbgcmd
0:000> c rgBuf1 (rgBuf1+0n100) rgBuf2

0:000> c rgBuf1 L 0n100 rgBuf2
```

 

 





