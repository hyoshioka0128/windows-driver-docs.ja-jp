---
title: srb
description: Srb の拡張機能には、SCSI 要求ブロック (SRB) についての情報が表示されます。
ms.assetid: 38f40a78-c991-465e-9203-a8171d1a86f6
keywords:
- Windows デバッグ srb
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- srb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 82286326ad1717073b0e778dd4d891596f1e9598
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334239"
---
# <a name="srb"></a>!srb


**! Srb**拡張機能は、SCSI 要求ブロック (SRB) についての情報を表示します。

```dbgcmd
!srb Address 
```

## <a name="span-idddksrbdbgspanspan-idddksrbdbgspanparameters"></a><span id="ddk__srb_dbg"></span><span id="DDK__SRB_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ターゲット コンピューターで、SRB の 16 進数のアドレスを指定します。

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

される Srb の詳細については、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

SRB は、SCSI ポート ドライバーに SCSI クラス ドライバーからの I/O 要求の通信に使用されるシステム定義の構造です。

 

 





