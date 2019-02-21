---
title: '\_DXGKARG\_CREATEALLOCATION2 構造体'
description: DXGKARG\_CREATEALLOCATION2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 4796f378-78e0-4119-9ab4-d25d61fca7de
keywords:
- _DXGKARG_CREATEALLOCATION2 構造体のディスプレイ デバイス
- DXGKARG_CREATEALLOCATION2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_CREATEALLOCATION2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a3ce3bafca4808e0df527a8e4359ebfee8314ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530864"
---
# <a name="dxgkargcreateallocation2-structure"></a>\_DXGKARG\_CREATEALLOCATION2 構造体


DXGKARG\_CREATEALLOCATION2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_CREATEALLOCATION2 {
  const VOID                  *pPrivateDriverData;
  UINT                        PrivateDriverDataSize;
  UINT                        NumAllocations;
  DXGK_ALLOCATIONINFO2        *pAllocationInfo;
  HANDLE                      hResource;
  DXGK_CREATEALLOCATIONFLAGS2 Flags;
} DXGKARG_CREATEALLOCATION2;
```

<a name="members"></a>Members
-------

**pPrivateDriverData**システム用に予約されています。

**PrivateDriverDataSize**システム用に予約されています。

**NumAllocations**システム用に予約されています。

**pAllocationInfo**システム用に予約されています。

**hResource**システム用に予約されています。

**フラグ**システム用に予約されています。

<a name="requirements"></a>要件
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

 

 





