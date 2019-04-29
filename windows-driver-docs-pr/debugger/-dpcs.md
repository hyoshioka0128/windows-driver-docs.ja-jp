---
title: dpc
description: Dpc 拡張機能は、指定されたプロセッサの遅延プロシージャ呼び出し (DPC) のキューを表示します。
ms.assetid: b5f71fb5-6fc7-4e8f-a439-1edb188e9876
keywords:
- DPC (遅延プロシージャ呼び出し)
- Windows デバッグ dpc
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpcs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dc1ffa6bbcade69f9d94847b745790d4a4b34eda
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334567"
---
# <a name="dpcs"></a>!dpcs


**! Dpc**拡張機能は、指定されたプロセッサの遅延プロシージャ呼び出し (DPC) のキューを表示します。

```dbgcmd
!dpcs [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサを指定します。 場合*プロセッサ*を省略すると、すべてのプロセッサの DPC キューが表示されます。

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
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Dpc については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 





