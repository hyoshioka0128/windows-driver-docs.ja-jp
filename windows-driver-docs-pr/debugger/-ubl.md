---
title: ubl
description: Ubl 拡張機能には、すべてのユーザー スペース ブレークポイントと現在の状態が一覧表示します。
ms.assetid: c2c40fa5-888f-49bb-a616-a139d7d2874d
keywords:
- ブレークポイント、ユーザー スペースのブレークポイント
- Windows デバッグ ubl
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ubl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c7f0bf65957902c5260c22242a1416d52e6f7829
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531442"
---
# <a name="ubl"></a>! ubl


**! Ubl**拡張機能には、すべてのユーザー スペース ブレークポイントと現在の状態が一覧表示されます。

```dbgcmd
!ubl
```

## <span id="ddk__ubl_dbg"></span><span id="DDK__UBL_DBG"></span>


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

ユーザー スペースのブレークポイントの表示と使用例を次に示します。

```dbgcmd
kd> !ubp 8014a131
This command is VERY DANGEROUS, and may crash your system!
If you don't know what you are doing, enter "!ubc *" now!

kd> !ubp 801544f4

kd> !ubd 1

kd> !ubl
 0: e ffffffff`8014a131 (ffffffff`82deb000) 1 ffffffff
 1: d ffffffff`801544f4 (ffffffff`82dff000) 0 ffffffff
```

この一覧内の各行には、ブレークポイントが含まれています数、状態 (**e**有効になっているまたは**d**無効の場合)、実際のブレークポイントの物理アドレスのブレークポイントを設定するために使用する仮想アドレス、。バイトの位置と、ブレークポイントの設定時にこのメモリ位置の内容。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**!ubc**](-ubc.md)

[**! スキャナー**](-ubd.md)

[**! ube**](-ube.md)

[**! ubp**](-ubp.md)

[ユーザー領域とシステム領域](user-space-and-system-space.md)

 

 






