---
title: '\_DXGKARG\_UPDATEPAGETABLE 構造体'
description: DXGKARG\_UPDATEPAGETABLE 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: abd5a200-5f10-4b5d-98e5-f75bc045aff8
keywords:
- _DXGKARG_UPDATEPAGETABLE 構造体のディスプレイ デバイス
- DXGKARG_UPDATEPAGETABLE 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGETABLE
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33e65321bae2be7635717182a87874c9135eee8b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578145"
---
# <a name="dxgkargupdatepagetable-structure"></a>\_DXGKARG\_UPDATEPAGETABLE 構造体


DXGKARG\_UPDATEPAGETABLE 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGETABLE {
  PVOID                        pPageTable;
  UINT                         SizeOfPageTableInPages;
  UINT                         StartIndex;
  UINT                         PageCount;
  const DXGK_PTE               *PTEArray;
  HANDLE                       hAllocation;
  UINT                         PageOffset;
  DXGKARG_UPDATEPAGETABLEFLAGS Flags;
} DXGKARG_UPDATEPAGETABLE;
```

<a name="members"></a>メンバー
-------

**pPageTable**システム用に予約されています。

**SizeOfPageTableInPages**システム用に予約されています。

**StartIndex**システム用に予約されています。

**PageCount**システム用に予約されています。

**PTEArray**システム用に予約されています。

**hAllocation**システム用に予約されています。

**PageOffset**システム用に予約されています。

**フラグ**システム用に予約されています。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows オペレーティング システムの以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmddi.h (include D3dkmddi.h)</td>
</tr>
</tbody>
</table>

 

 





