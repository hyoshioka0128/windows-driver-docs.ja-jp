---
title: arbinst
description: Arbinst 拡張機能には、指定した監視についての情報が表示されます。
ms.assetid: 6aa06283-9cd7-4579-9e5d-40bbaf53f782
keywords:
- 監視
- Windows デバッグ arbinst
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- arbinst
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e4f4d1161fbfa5b167c0b82fb96274d44b158f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557292"
---
# <a name="arbinst"></a>! arbinst


**! Arbinst**拡張機能には、指定した監視についての情報が表示されます。

```dbgcmd
    !arbinst Address [Flags]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="Address"></span><span id="address"></span><span id="ADDRESS"></span>*アドレス*  
表示するためにアービターの 16 進数のアドレスを指定します。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>*フラグ*  
各監視用に表示する情報の量を指定します。 現在、唯一のフラグは 0x100 です。 このフラグが設定されている場合は、エイリアスが表示されます。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


参照してください、 [ **! アービター** ](-arbiter.md)拡張機能。

<a name="remarks"></a>注釈
-------

指定すると、監視の **! arbinst** PDO が範囲 (つまり、範囲の所有者)、およびこの所有者のサービス名に接続されている (わかる場合) にシステム リソースをいくつかのオプション フラグの範囲を割り当てる各が表示されます。

以下に例を示します。

```console
kd> !arbinst e0000106002ee8e8
Port Arbiter "PCI I/O Port (b=02)" at e0000106002ee8e8
  Allocated ranges:
    0000000000000000 - 0000000000001fff       00000000 <Not on bus>
    0000000000002000 - 00000000000020ff     P e0000000858bea20  (ql1280)
    0000000000003000 - ffffffffffffffff       00000000 <Not on bus>
  Possible allocation:
    < none >
kd> !arbinst e0000106002ec458
Memory Arbiter "PCI Memory (b=02)" at e0000106002ec458
  Allocated ranges:
    0000000000000000 - 00000000ebffffff       00000000 <Not on bus>
    00000000effdef00 - 00000000effdefff   B   e0000000858be560 
    00000000effdf000 - 00000000effdffff       e0000000858bea20  (ql1280)
    00000000f0000000 - ffffffffffffffff       00000000 <Not on bus>
  Possible allocation:
    < none >
```

 

 





