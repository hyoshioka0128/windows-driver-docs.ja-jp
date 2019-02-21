---
title: minipkd.adapter
description: Minipkd.adapter 拡張機能には、指定したアダプタについての情報が表示されます。
ms.assetid: 86cde6f0-9690-41b6-8e81-b9d25d7d6de5
keywords:
- デバッグ minipkd.adapter Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.adapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c91403ee1ee2a3a8c8989597be64118fa23ced36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529799"
---
# <a name="minipkdadapter"></a>! minipkd.adapter


**! Minipkd.adapter**拡張機能は、指定したアダプターに関する情報を表示します。

```dbgcmd
!minipkd.adapter Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
アダプターのアドレスを指定します。

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

<a name="remarks"></a>注釈
-------

アダプターのアドレスが記載されて、 **DevExt**のフィールド、 [ **! minipkd.adapters** ](-minipkd-adapters.md)を表示します。

 

 





