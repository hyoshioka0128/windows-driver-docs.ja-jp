---
title: chklowmem
description: Chklowmem 拡張機能は、4 GB 未満の物理メモリのページが、/pae および/nolowmem オプションを使用して起動されているコンピューターで必要な塗りつぶしのパターンで塗りつぶされますかどうかを判断します。
ms.assetid: cc1054e2-b824-4fcf-b353-9ee8c0d3dbf3
keywords:
- PAE (物理アドレス拡張)
- Windows デバッグ chklowmem
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- chklowmem
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fd654f9e840d118313a262ddf6daa49df6e78871
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363167"
---
# <a name="chklowmem"></a>!chklowmem


**! Chklowmem**拡張機能では、4 GB 未満の物理メモリのページが必要な塗りつぶしのパターンを使用して起動されているコンピューターに格納されるかどうかを決定、 [ **/pae** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/-pae)[ **/nolowmem** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/-nolowmem)オプション。

```dbgsyntax
!chklowmem
```

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

この拡張機能は、カーネル モード ドライバーが 4 GB の境界を超える物理メモリ適切に動作を確認する場合に便利です。 通常、ドライバーは、32 ビットにし、4 GB の境界の下で、物理アドレスを切り捨てることで失敗します。 **! Chklowmem**拡張機能は 4 GB の境界下のすべての書き込みを検出します。

 

 





