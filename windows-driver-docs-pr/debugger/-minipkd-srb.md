---
title: minipkd.srb
description: Minipkd.srb 拡張機能には、指定された SCSI 要求のブロック (SRB) のデータ構造が表示されます。
ms.assetid: d742a900-f8a8-43a8-b00a-12bb82ca1460
keywords:
- デバッグ minipkd.srb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.srb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d6bcfcb541230dec79bc5653d93a71e3968b7ec0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336035"
---
# <a name="minipkdsrb"></a>!minipkd.srb


**! Minipkd.srb**拡張機能には、指定された SCSI 要求ブロック (SRB) のデータ構造が表示されます。

```dbgcmd
!minipkd.srb SRB 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______SRB______"></span><span id="_______srb______"></span> *SRB*   
SRB のアドレスを指定します。

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
<td align="left"><p>Minipkd.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

詳細については、次を参照してください。 [SCSI ミニポート デバッグ](scsi-miniport-debugging.md)します。

<a name="remarks"></a>コメント
-------

現在アクティブな要求のすべてのアドレスが記載されて、 *SRB*からの出力のフィールド、 [ **! minipkd.req** ](-minipkd-req.md)コマンド。

この拡張機能は、SCSI、SRB およびそのアドレスと 16 進数のフラグ値を発行するアドレスは、ドライバー、SRB の状態を表示します。 0x10000 がフラグの値に設定されている場合この要求は現在、ミニポートです。

 

 





