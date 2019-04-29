---
title: tzinfo
description: Tzinfo 拡張機能には、指定された温度のゾーン情報構造体の内容が表示されます。
ms.assetid: a30826d8-b7c5-4fbc-a3c3-b7a994eaf7fe
keywords:
- 温度のゾーン情報
- Windows デバッグ tzinfo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tzinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 645e44da4cd98121b0be693c27f3437b1c10e877
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334165"
---
# <a name="tzinfo"></a>!tzinfo


**! Tzinfo**拡張機能には、指定された温度のゾーン情報構造体の内容が表示されます。

```dbgcmd
!tzinfo Address
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する温度のゾーン情報の構造体のアドレス。

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

表示するには、システムの電源機能を使用して、 [ **! pocaps** ](-pocaps.md)拡張機能コマンド。 表示するには、システムの電源ポリシーを使用して、 [ **! popolicy** ](-popolicy.md)拡張機能コマンド。 電源機能、および電源ポリシーについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

 

 





