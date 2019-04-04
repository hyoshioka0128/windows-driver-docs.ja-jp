---
title: sysptes
description: Sysptes 拡張機能では、システム ページ テーブル エントリ (Pte) の書式設定されたビューが表示されます。
ms.assetid: cfb40732-6658-43aa-8b83-0ad4b55194ba
keywords:
- Windows デバッグ sysptes
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sysptes
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 75066ef7201fb1112eeb1f26145ca310e4166c98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580186"
---
# <a name="sysptes"></a>!sysptes


**! Sysptes**拡張機能には、システム ページ テーブル エントリ (Pte) の書式設定されたビューが表示されます。

```dbgcmd
!sysptes [Flags]
```

## <a name="span-idddksysptesdbgspanspan-idddksysptesdbgspanparameters"></a><span id="ddk__sysptes_dbg"></span><span id="DDK__SYSPTES_DBG"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示する詳細レベルを指定します。 *フラグ*次のビットの組み合わせにすることができます。 既定値は、0 です。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
無料 Pte についての情報を表示します。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
(Windows 2000 のみ)ページの使用状況の統計では、未使用のページを表示します。

グローバルの特別なプールに空き Pte についての情報を表示します。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
ロックされたページを任意のシステムのマッピングに割り当てられている Pte について詳細な情報を表示します。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
(Windows 2000 および Windows XP の場合のみ)非ページ プールの拡張の無料 PTE 情報が表示されます。 このビットが設定されている場合、他のリストは表示されません。 0x1 と 0x8 の両方が設定すると、すべての非ページ プールの拡張が無料である場合は、Pte が表示されます。 0x8 が設定されている場合のみ、合計のみが表示されます。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
(Windows Vista 以降)セッションの特別なプールの空き PTE 情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ページのテーブルと Pte については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 

<a name="remarks"></a>コメント
-------

特定の PTE を確認するを使用して、 [ **! pte** ](-pte.md)拡張機能。

Windows システムから例を次に示します。

```dbgcmd
kd> !sysptes 1

System PTE Information
  Total System Ptes 571224
     SysPtes list of size 1 has 361 free
     SysPtes list of size 2 has 91 free
     SysPtes list of size 4 has 48 free
     SysPtes list of size 8 has 36 free
     SysPtes list of size 9 has 29 free
     SysPtes list of size 23 has 29 free
 
    starting PTE: fffffe0059388000
    ending PTE:   fffffe00597e3ab8

      free ptes: fffffe0059388000   number free: 551557.
      free ptes: fffffe00597be558   number free: 104.
      free ptes: fffffe00597d2828   number free: 676.

  free blocks: 3   total free: 552337    largest free block: 551557
```

 

 





