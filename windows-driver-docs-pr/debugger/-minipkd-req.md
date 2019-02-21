---
title: minipkd.req
description: Minipkd.req 拡張機能では、指定されたアダプターまたはデバイスで現在アクティブな要求のすべてに関する情報が表示されます。
ms.assetid: 5edc00dd-9a0b-4576-a3ec-11ce22163e95
keywords:
- デバッグ minipkd.req Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.req
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a1bfc79973c5aa23d3d92e762ce5e8258ea0c3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531423"
---
# <a name="minipkdreq"></a>!minipkd.req


**! Minipkd.req**拡張機能は、指定されたアダプターまたはデバイスのすべての現在アクティブな要求に関する情報を表示します。

```dbgcmd
!minipkd.req Adapter 
!minipkd.req Device 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Adapter______"></span><span id="_______adapter______"></span><span id="_______ADAPTER______"></span> *アダプター*   
アダプターのアドレスを指定します。

<span id="_______Device______"></span><span id="_______device______"></span><span id="_______DEVICE______"></span> *デバイス*   
論理ユニットの拡張機能 (LUN) デバイスの物理デバイス オブジェクト (PDO) を指定します。

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

LUN の PDO が記載されて、 **DevObj**のフィールド、 [ **! minipkd.adapters** ](-minipkd-adapters.md)を表示します。

 

 





