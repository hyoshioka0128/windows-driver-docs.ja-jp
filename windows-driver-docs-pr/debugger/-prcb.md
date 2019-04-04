---
title: prcb
description: Prcb 拡張機能では、プロセッサの制御ブロック (PRCB) が表示されます。
ms.assetid: 747695a1-8a5d-4d30-9315-91f4bf7f568e
keywords:
- プロセッサのコントロール ブロック
- Windows デバッグ prcb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- prcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d28eb002f743c2382c3a899a65eda6abbaebe550
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535863"
---
# <a name="prcb"></a>! prcb


**! Prcb**拡張機能には、プロセッサの制御ブロック (PRCB) が表示されます。

```dbgcmd
!prcb [Processor]
```

## <a name="span-idddkprcbdbgspanspan-idddkprcbdbgspanparameters"></a><span id="ddk__prcb_dbg"></span><span id="DDK__PRCB_DBG"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
PRCB 情報を取得するプロセッサを指定します。 場合*プロセッサ*は省略すると、プロセッサ 0 が使用されます。

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

PCR、および、PRCB については、*Microsoft Windows internals 』*、Mark Russinovich と David Solomon を参照してください。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

PRCB は、プロセッサのコントロールの領域 (PCR) の拡張です。 表示するには、PCR を使用して、 [ **! pcr** ](-pcr.md)拡張機能。

以下に例を示します。

```dbgcmd
kd> !prcb
PRCB for Processor 0 at e0000000818ba000:
Threads--  Current e0000000818bbe10 Next 0000000000000000 Idle e0000000818bbe10
Number 0 SetMember 00000001
Interrupt Count -- 0000b81f
Times -- Dpc    00000028 Interrupt 000003ff 
         Kernel 00005ef4 User      00000385 
```

 

 





