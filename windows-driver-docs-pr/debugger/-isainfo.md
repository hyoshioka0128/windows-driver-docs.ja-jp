---
title: isainfo
description: Isainfo 拡張機能は、PNPISA カードについての情報を表示します。 または、デバイスでは、システムで提示.
ms.assetid: 8caa501e-3bb7-4af8-a7ea-e8b255b9f24c
keywords:
- I/O バス
- CARD_INFORMATION
- Windows デバッグ isainfo
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- isainfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae347aa0f24202db04c121fe40094255c85d6d8b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336431"
---
# <a name="isainfo"></a>!isainfo


**! Isainfo** PNPISA カードについての情報を表示拡張機能またはデバイスでは、システムで提示.

```dbgcmd
!isainfo [Card]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Card______"></span><span id="_______card______"></span><span id="_______CARD______"></span> *カード*   
PNPISA カードを指定します。 場合*カード*が 0 または省略すると、すべてのデバイスと PNPISA (つまり、PC I/O) バス上のカードが表示されます。

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

 

<a name="remarks"></a>注釈
-------

この拡張機能からの出力の例を次に示します。

```dbgcmd
0: kd> !isainfo
ISA PnP FDO @ 0x867b9938, DevExt @ 0x867b99f0, Bus # 0
Flags (0x80000000)  DF_BUS

  ISA PnP PDO @ 0x867B9818, DevExt @ 0x86595388
  Flags (0x40000818)  DF_ENUMERATED, DF_ACTIVATED, 
                      DF_REQ_TRIMMED, DF_READ_DATA_PORT
```

 

 





