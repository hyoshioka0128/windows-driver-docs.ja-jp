---
title: pte2va
description: Pte2va 拡張機能では、指定したページ テーブル エントリ (PTE) に対応する仮想アドレスが表示されます。
ms.assetid: 9a94ce3a-dbbc-4566-9ef5-3ec76c1505eb
keywords:
- デバッグ pte2va Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pte2va
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0582e1cffaad68efee46529b86b3f8915f09f6cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552531"
---
# <a name="pte2va"></a>! pte2va


**! Pte2va**拡張機能は、指定したページ テーブル エントリ (PTE) に対応する仮想アドレスを表示します。

```dbgcmd
!pte2va Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
PTE を指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ページのテーブルと Pte については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (この本できない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

特定の PTE の内容を確認するを使用して、 [ **! pte** ](-pte.md)拡張機能。

出力の例を次に示します、 **! pte2va**拡張機能。

```dbgcmd
kd> !pte2va 9230
000800000248c000 
```

 

 





