---
title: qlocks
description: Qlocks 拡張機能は、すべてのキューに置かれたスピン ロックの状態を表示します。
ms.assetid: fdeefedb-c840-410a-94e4-ae42923e82e7
keywords:
- Windows デバッグ qlocks
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- qlocks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 475431764925dd6e584f9099173963c23c505c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334331"
---
# <a name="qlocks"></a>!qlocks


**! Qlocks**拡張機能には、すべてのキューに置かれたスピン ロックの状態が表示されます。

```dbgcmd
!qlocks 
```

## <span id="ddk__qlocks_dbg"></span><span id="DDK__QLOCKS_DBG"></span>


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

スピン ロックについては、Windows Driver Kit (WDK) ドキュメントを参照してくださいと*Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

このコマンドは、マルチプロセッサ システムでのみ有効です。

以下に例を示します。

```dbgcmd
0: kd> !qlocks
Key: O = Owner, 1-n = Wait order, blank = not owned/waiting, C = Corrupt

                       Processor Number
    Lock Name         0  1  2  3

KE   - Dispatcher               
KE   - Unused Spare             
MM   - PFN                      
MM   - System Space             
CC   - Vacb                     
CC   - Master                   
EX   - NonPagedPool             
IO   - Cancel                   
EX   - WorkQueue                
IO   - Vpb                      
IO   - Database                 
IO   - Completion               
NTFS - Struct                   
AFD  - WorkQueue                
CC   - Bcb                      
MM   - MM NonPagedPool             
```

 

 





