---
title: minipkd.portconfig
description: Minipkd.portconfig 拡張機能では、指定した PORT_CONFIGURATION_INFORMATION データ構造に関する情報が表示されます。
ms.assetid: efc527c4-0340-4976-9126-d3e32286fc64
keywords:
- デバッグ minipkd.portconfig Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- minipkd.portconfig
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1dc61790f8281c6260401b979198b2ed833f7c4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336087"
---
# <a name="minipkdportconfig"></a>!minipkd.portconfig


**! Minipkd.portconfig**拡張機能には、指定されたポートに関する情報が表示されます。\_構成\_情報データの構造体。

```dbgcmd
!minipkd.portconfig PortConfig 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______PortConfig______"></span><span id="_______portconfig______"></span><span id="_______PORTCONFIG______"></span> *PortConfig*   
ポートのアドレスを指定します\_構成\_情報データの構造体。

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

*PortConfig*でアドレスがあります、**ポートの構成情報**のフィールド、 [ **! minipkd.adapter** ](-minipkd-adapter.md)を表示します。

 

 





