---
title: pocaps
description: Pocaps 拡張機能では、ターゲット コンピューターの電源機能が表示されます。
ms.assetid: 011d923a-a5c4-4d3b-ba06-fe5dc884adaa
keywords:
- Windows デバッグ pocaps
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pocaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ce187373b0432aafe41db47c05efd427d8f8f70f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335776"
---
# <a name="pocaps"></a>!pocaps


**! Pocaps**拡張機能には、ターゲット コンピューターの電源機能が表示されます。

```dbgcmd
!pocaps
```

## <span id="ddk__pocaps_dbg"></span><span id="DDK__POCAPS_DBG"></span>


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

表示するには、システムの電源ポリシーを使用して、 [ **! popolicy** ](-popolicy.md)拡張機能コマンド。 電源機能、および電源ポリシーについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)

<a name="remarks"></a>注釈
-------

このコマンドの出力の例を次に示します。

```dbgcmd
kd> !pocaps
PopCapabilities @ 0x8016b100
  Misc Supported Features:  S4 FullWake
  Processor Features:      
  Disk Features:            SpinDown
  Battery Features:        
  Wake Caps
    Ac OnLine Wake:         Sx
    Soft Lid Wake:          Sx
    RTC Wake:               Sx
    Min Device Wake:        Sx
    Default Wake:           Sx
```

 

 





