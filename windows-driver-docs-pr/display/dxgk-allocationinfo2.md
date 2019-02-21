---
title: '\_DXGK\_ALLOCATIONINFO2 構造体'
description: DXGK\_ALLOCATIONINFO2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: af396dd1-6b47-4724-a481-c8f4646816e9
keywords:
- _DXGK_ALLOCATIONINFO2 構造体のディスプレイ デバイス
- DXGK_ALLOCATIONINFO2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONINFO2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 23c1e8d305312dfa6750d7b313a1626c038147c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551354"
---
# <a name="dxgkallocationinfo2-structure"></a>\_DXGK\_ALLOCATIONINFO2 構造体


DXGK\_ALLOCATIONINFO2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONINFO2 {
  VOID                      *pPrivateDriverData;
  UINT                      PrivateDriverDataSize;
  UINT                      Alignment;
  SIZE_T                    Size;
  DXGK_SEGMENTPREFERENCE    PreferredSegment;
  UINT                      SupportedSegmentSet;
  UINT                      MaximumRenamingListLength;
  HANDLE                    hAllocation;
  DXGK_ALLOCATIONINFOFLAGS2 Flags;
  DXGK_ALLOCATIONUSAGEHINT  *pAllocationUsageHint;
  UINT                      AllocationPriority;
  UINT                      AllocationGroup;
  UINT                      SwizzlingInvariantBlockSize;
  UINT                      Reserved[6];
} DXGK_ALLOCATIONINFO2;
```

<a name="members"></a>Members
-------

**pPrivateDriverData**システム用に予約されています。

**PrivateDriverDataSize**システム用に予約されています。

**配置**システム用に予約されています。

**サイズ**システム用に予約されています。

**PreferredSegment**システム用に予約されています。

**SupportedSegmentSet**システム用に予約されています。

**MaximumRenamingListLength**システム用に予約されています。

**hAllocation**システム用に予約されています。

**フラグ**システム用に予約されています。

**pAllocationUsageHint**システム用に予約されています。

**AllocationPriority**システム用に予約されています。

**AllocationGroup**システム用に予約されています。

**SwizzlingInvariantBlockSize**システム用に予約されています。

**予約済み**システム用に予約されています。

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

 

 





