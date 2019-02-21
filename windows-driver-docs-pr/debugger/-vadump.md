---
title: vadump
description: Vadump の拡張機能では、すべての仮想メモリの範囲とその対応する保護情報が表示されます。
ms.assetid: b13aa852-7333-41fc-ad66-4386040522d8
keywords:
- Windows デバッグ vadump
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- vadump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 827b41c8afbd9188f9c41edd072e50012abecb11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538803"
---
# <a name="vadump"></a>! vadump


**! Vadump**拡張機能は、すべての仮想メモリの範囲とその対応する保護情報が表示されます。

```dbgcmd
    !vadump [-v] 
```

## <a name="span-idddkvadumpdbgspanspan-idddkvadumpdbgspanparameters"></a><span id="ddk__vadump_dbg"></span><span id="DDK__VADUMP_DBG"></span>パラメーター


<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
それぞれの元の割り当てリージョンにも情報を含めるようにディスプレイをによりします。 リージョン内の個々 のアドレスは、メモリが割り当てられた後に変更される、保護を持つことができます (によって**VirtualProtect**など)、このリージョンの元の保護の状態できない可能性がありますをそれぞれのと同じです。リージョン内の範囲です。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

1 つの仮想アドレスのメモリ保護情報を表示する使用[ **! vprot**](-vprot.md)します。 メモリ保護については、次を参照してください。 *Microsoft Windows internals 』* Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

以下に例を示します。

```dbgcmd
0:000> !vadump
BaseAddress:       00000000
RegionSize:        00010000
State:             00010000  MEM_FREE
Protect:           00000001  PAGE_NOACCESS

BaseAddress:       00010000
RegionSize:        00001000
State:             00001000  MEM_COMMIT
Protect:           00000004  PAGE_READWRITE
Type:              00020000  MEM_PRIVATE
.........
```

この表示では、状態の行は、メモリ範囲開始位置として、指定したベース アドレスの状態を示します。 可能な状態値はメモリ最適化\_コミット、メモリ最適化\_無償商品、およびメモリ最適化\_予約します。

保護する行には、このメモリの範囲の保護状態が表示されます。 保護可能な値はページ\_NOACCESS、ページ\_READONLY、ページ\_READWRITE、ページ\_EXECUTE、ページ\_EXECUTE\_読み取り、ページ\_EXECUTE\_READWRITE、ページ\_WRITECOPY、ページ\_EXECUTE\_WRITECOPY、およびページ\_ガード。

型の行では、メモリの種類を示します。 使用可能な値はメモリ最適化\_イメージ、メモリ最適化\_マップ済み、およびメモリ最適化\_プライベートです。

例を次に示しますを使用して、 **-v**パラメーター。

```dbgcmd
0:000> !vadump -v
BaseAddress:       00000000
AllocationBase:    00000000
RegionSize:        00010000
State:             00010000  MEM_FREE
Protect:           00000001  PAGE_NOACCESS

BaseAddress:       00010000
AllocationBase:    00010000
AllocationProtect: 00000004  PAGE_READWRITE
RegionSize:        00001000
State:             00001000  MEM_COMMIT
Protect:           00000004  PAGE_READWRITE
Type:              00020000  MEM_PRIVATE
.........
```

ときに **-v** AllocationProtect 行では、既定値を示しています。 使用領域全体が作成された保護します。 保護する行は、この特定のアドレスの実際の保護を示しています。

 

 





