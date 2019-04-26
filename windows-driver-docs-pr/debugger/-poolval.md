---
title: poolval
description: Poolval 拡張機能では、プール ページのヘッダーを分析し、破損している可能性を診断します。 この拡張機能は Windows XP およびそれ以降のバージョンで使用できます。
ms.assetid: b67ab2d4-c765-4721-81ed-c6b7c9a0ba6d
keywords:
- Windows デバッグ poolval
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- poolval
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3874c69e83ea9c6a3c9e5bdfdd3fa1e0d015ce52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335807"
---
# <a name="poolval"></a>!poolval


**! Poolval**拡張機能がプール ページのヘッダーを分析し、破損している可能性を診断します。 この拡張機能は Windows XP およびそれ以降のバージョンで使用できます。

```dbgcmd
!poolval Address [DisplayLevel]
```

## <a name="span-idddkpoolvaldbgspanspan-idddkpoolvaldbgspanparameters"></a><span id="ddk__poolval_dbg"></span><span id="DDK__POOLVAL_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ヘッダーは、分析するプールのアドレスを指定します。

<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
表示に含める情報を指定します。 (既定値は 0) 値は次のいずれかを指定できます。

<span id="0"></span>0  
基本的な情報が表示されます。

<span id="1"></span>1  
表示されるエラーの原因の基本的な情報とリンク ヘッダーが一覧表示します。

<span id="2"></span>2  
により基本情報、リンク ヘッダーのリスト、および基本的なヘッダー情報を表示します。

<span id="3"></span>3  
により基本情報、リンク ヘッダーのリスト、およびすべてのヘッダー情報を表示します。

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

メモリ プールの詳細については、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 





