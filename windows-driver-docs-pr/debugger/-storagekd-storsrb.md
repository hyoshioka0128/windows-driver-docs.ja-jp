---
title: storagekd.storsrb
description: Storagekd.storsrb 拡張機能には、指定されたストレージ (または SCSI) に関する情報が表示されます。 ブロックの要求 (SRB)。
ms.assetid: E2AB3BE2-0EE1-4FB5-9F62-02169B22B00B
keywords:
- デバッグ storagekd.storsrb Windows
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storsrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 67a04170a375b54f772a584566f6ad815cea4fd0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559007"
---
# <a name="storagekdstorsrb"></a>!storagekd.storsrb


**! Storagekd.storsrb**拡張機能には、指定されたストレージ (または SCSI) に関する情報が表示されます。 ブロックの要求 (SRB)。

```dbgcmd
!storagekd.storsrb Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Address"></span><span id="_______address"></span><span id="_______ADDRESS"></span> *アドレス*  
SRB のアドレスを指定します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 以降</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

次の例に示します、 **! storagekd.storsrb**表示。

**0: kd&gt; !storagekd.storsrb ffffe00111fe25b0**

```dbgcmd
    SRB is a STORAGE request block (SRB_EX)
    SRB EX 0xffffe00111fe25b0 Function 28  Version  1, Signature 53524258, SrbStatus: 0x02[Aborted], SrbFunction 0x00 [EXECUTE SCSI]
    Address Type is BTL8

       SRB_EX Data Type [SrbExDataTypeScsiCdb16] 
    [EXECUTE SCSI] SRB_EX: 0xffffe00111fe2648  OriginalRequest: 0xffffe001125a9010  DataBuffer/Length: 0xffffe00112944000 / 0x00000200
    PTL: (0, 1, 1)  CDB: 28 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00  OpCode: SCSI/READ (10)   
```

 

 





