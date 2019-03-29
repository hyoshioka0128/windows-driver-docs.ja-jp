---
title: '\_DXGKARG\_UPDATEPAGEDIRECTORY 構造体'
description: DXGKARG\_UPDATEPAGEDIRECTORY 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: ac16c040-50d8-4716-8275-682092a2be77
keywords:
- _DXGKARG_UPDATEPAGEDIRECTORY 構造体のディスプレイ デバイス
- DXGKARG_UPDATEPAGEDIRECTORY 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGEDIRECTORY
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a34da191de818a172c14f5cd99e5544ec8dcd225
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570859"
---
# <a name="dxgkargupdatepagedirectory-structure"></a>\_DXGKARG\_UPDATEPAGEDIRECTORY 構造体


DXGKARG\_UPDATEPAGEDIRECTORY 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGEDIRECTORY {
  PVOID          pPageDirectory;
  UINT           StartIndex;
  UINT           PageTableCount;
  const DXGK_PDE *PDEArray;
} DXGKARG_UPDATEPAGEDIRECTORY;
```

<a name="members"></a>メンバー
-------

**pPageDirectory**システム用に予約されています。

**StartIndex**システム用に予約されています。

**PageTableCount**システム用に予約されています。

**PDEArray**システム用に予約されています。

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

 

 





