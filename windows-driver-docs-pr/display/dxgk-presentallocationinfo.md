---
title: DXGK\_PRESENTALLOCATIONINFO 構造体
description: DXGK\_PRESENTALLOCATIONINFO 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 8a7f25cf-c08c-4f65-bbf4-ba129d88ff6a
keywords:
- DXGK_PRESENTALLOCATIONINFO 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_PRESENTALLOCATIONINFO
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 360e4c8978e9ddc4f98bfaeb4528fd59dbce3cee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392032"
---
# <a name="dxgkpresentallocationinfo-structure"></a>DXGK\_PRESENTALLOCATIONINFO 構造体


DXGK\_PRESENTALLOCATIONINFO 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_PRESENTALLOCATIONINFO {
  HANDLE                 hDeviceSpecificAllocation;
  D3DGPU_VIRTUAL_ADDRESS AllocationVirtualAddress;
  PHYSICAL_ADDRESS       PhysicalAddress;
  WORD                   SegmentId;
  WORD                   PhysicalAdapterIndex;
} DXGK_PRESENTALLOCATIONINFO;
```

<a name="members"></a>メンバー
-------

**hDeviceSpecificAllocation**システム用に予約されています。

**AllocationVirtualAddress**システム用に予約されています。

**PhysicalAddress**システム用に予約されています。

**SegmentId**システム用に予約されています。

**PhysicalAdapterIndex**システム用に予約されています。

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

 

 





