---
title: pocaps
description: Pocaps 拡張機能には、対象のコンピューターの電源機能が表示されます。
ms.assetid: 011d923a-a5c4-4d3b-ba06-fe5dc884adaa
keywords:
- pocaps Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pocaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d67f865c12ff33d5e347774ed7f809d9ef8727c
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025191"
---
# <a name="pocaps"></a>!pocaps


**! Pocaps**拡張機能には、対象のコンピューターの電源機能が表示されます。

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
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

システムの電源ポリシーを表示するには、 [ **! popolicy**](-popolicy.md)拡張コマンドを使用します。 電源機能と電源ポリシーの詳細については、Windows Driver Kit (WDK) のドキュメントと*Microsoft windows の内部構造*を参照してください。これには、Mark Russinovich と David ソロモンが使用されます。

<a name="remarks"></a>コメント
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

 

 





