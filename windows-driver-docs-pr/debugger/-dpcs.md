---
title: dpc
description: Dpc 拡張機能は、指定されたプロセッサの遅延プロシージャ呼び出し (DPC) キューを表示します。
ms.assetid: b5f71fb5-6fc7-4e8f-a439-1edb188e9876
keywords:
- DPC (遅延プロシージャ呼び出し)
- dpc Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dpcs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 79833c0723cf1c7a30ad8c0a03a1b8595e3031d8
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025268"
---
# <a name="dpcs"></a>!dpcs


**! Dpc**拡張機能は、指定されたプロセッサの遅延プロシージャ呼び出し (DPC) キューを表示します。

```dbgcmd
!dpcs [Processor]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメータ


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*プロセッサ*   
プロセッサを指定します。 *プロセッサ*を省略すると、すべてのプロセッサの DPC キューが表示されます。

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
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Dpc の詳細については、Windows Driver Kit (WDK) のドキュメントおよび*Microsoft windows の内部*(Mark Russinovich と David ソロモン) を参照してください。

 

 





