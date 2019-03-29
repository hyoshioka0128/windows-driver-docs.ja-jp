---
title: memlist
description: Memlist 拡張機能は、それらの整合性をチェックするためにページ フレームの数 (PFN) のデータベースからの物理メモリの一覧をスキャンします。
ms.assetid: 9d5307df-5e46-4d95-8c96-ab6da0f54cd0
keywords:
- PFN データベース
- Windows デバッグ memlist
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- memlist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90b8b877ec4f6e8cbb6b9be8015f7a49dd528862
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571694"
---
# <a name="memlist"></a>!memlist


**! Memlist**拡張機能は、それらの整合性をチェックするためにページ フレームの数 (PFN) のデータベースからの物理メモリの一覧をスキャンします。

```dbgcmd
!memlist Flags
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
メモリの一覧を確認するを指定します。 現時点では、1 つの値が実装されています。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
検証するゼロ ページ リストをによりします。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

現時点では、この拡張機能は、そのリスト内のすべてのページがゼロになっていることを確認するゼロ ページ リストをのみ確認されます。 適切な構文です。

```dbgcmd
kd> !memlist 1
```

 

 





