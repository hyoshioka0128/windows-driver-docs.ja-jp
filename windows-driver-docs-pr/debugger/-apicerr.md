---
title: apicerr
description: Apicerr 拡張機能は、ローカルの高度なプログラミング可能な割り込みコント ローラー (APIC) エラー ログを表示します。
ms.assetid: b058412b-a4df-42cc-8550-b5db4e0bbccc
keywords:
- APIC (Advanced Programmable Interrupt Controller)
- Windows デバッグ apicerr
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- apicerr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b5e12eb86820eb4ffedd60e1991882500d323c9f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334735"
---
# <a name="apicerr"></a>!apicerr


**! Apicerr**拡張機能は、ローカルの高度なプログラミング可能な割り込みコント ローラー (APIC) エラー ログを表示します。

```dbgcmd
     !apicerr [Format] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Format______"></span><span id="_______format______"></span><span id="_______FORMAT______"></span> *書式設定*   
エラー ログの内容を表示する順序を指定します。 次の値のいずれかこのことができます。

<span id="0x0"></span><span id="0X0"></span>0x0  
見つかった位置の順序に従って、エラー ログを表示します。

<span id="0x1"></span><span id="0X1"></span>0x1  
プロセッサに応じて、エラー ログを表示します。

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

 

この拡張機能のコマンドは、x86 ベースまたは x64 ベースの移行先コンピューターでのみ使用できます。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Apic のパフォーマンスについては、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 

 

 





