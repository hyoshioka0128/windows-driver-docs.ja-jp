---
title: prcb
description: Prcb 拡張機能は、プロセッサ制御ブロック (PRCB) を表示します。
ms.assetid: 747695a1-8a5d-4d30-9315-91f4bf7f568e
keywords:
- プロセッサ制御ブロック
- prcb Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- prcb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3ebc3a1ec42dcc84e3047046db859698fdaed04e
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025181"
---
# <a name="prcb"></a>!prcb


**! Prcb**拡張機能により、プロセッサ制御ブロック (prcb) が表示されます。

```dbgcmd
!prcb [Processor]
```

## <a name="span-idddk__prcb_dbgspanspan-idddk__prcb_dbgspanparameters"></a><span id="ddk__prcb_dbg"></span><span id="DDK__PRCB_DBG"></span>パラメータ


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*プロセッサ*   
PRCB 情報を取得するプロセッサを指定します。 *プロセッサ*を省略した場合は、プロセッサ0が使用されます。

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
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

PCR と PRCB の詳細については、「 *Microsoft Windows の内部*」 (Mark Russinovich と David ソロモン) を参照してください。

<a name="remarks"></a>コメント
-------

PRCB は、プロセッサ制御領域 (PCR) の拡張機能です。 PCR を表示するには、 [ **! pcr**](-pcr.md)拡張機能を使用します。

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

 

 





