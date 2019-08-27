---
title: poolval
description: Poolval 拡張機能は、プールページのヘッダーを分析し、可能性のある破損を診断します。 この拡張機能は、Windows XP 以降のバージョンでのみ使用できます。
ms.assetid: b67ab2d4-c765-4721-81ed-c6b7c9a0ba6d
keywords:
- poolval Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a25bcbd1762b1c4e58defd28552c31fdc3f18a2
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025196"
---
# <a name="poolval"></a>!poolval


**! Poolval**拡張機能は、プールページのヘッダーを分析し、可能性のある破損を診断します。 この拡張機能は、Windows XP 以降のバージョンでのみ使用できます。

```dbgcmd
!poolval Address [DisplayLevel]
```

## <a name="span-idddk__poolval_dbgspanspan-idddk__poolval_dbgspanparameters"></a><span id="ddk__poolval_dbg"></span><span id="DDK__POOLVAL_DBG"></span>パラメータ


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
ヘッダーが分析されるプールのアドレスを指定します。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*Displaylevel*   
表示に含める情報を指定します。 次のいずれかの値を指定できます (既定値は0です)。

<span id="0"></span>0  
基本情報が表示されます。

<span id="1"></span>1  
基本情報およびリンクされたヘッダーリストが表示されます。

<span id="2"></span>3  
基本情報、リンクされたヘッダーリスト、および基本ヘッダー情報を表示します。

<span id="3"></span>番  
基本情報、リンクされたヘッダーリスト、およびすべてのヘッダー情報を表示します。

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

メモリプールの詳細については、「Windows Driver Kit (WDK)」のドキュメントと*Microsoft windows の内部構造*を参照してください。これには、Mark Russinovich と David ソロモンが使用されます。

 

 





