---
title: '\_DXGK\_ALLOCATIONGROUPOUT 構造体'
description: DXGK\_ALLOCATIONGROUPOUT 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 4aafe036-09a5-4e2d-a2ea-b81d0ba05ec1
keywords:
- _DXGK_ALLOCATIONGROUPOUT 構造体のディスプレイ デバイス
- DXGK_ALLOCATIONGROUPOUT 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONGROUPOUT
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcad8a968f450ff2ee47812606936f15529e7db5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571984"
---
# <a name="dxgkallocationgroupout-structure"></a>\_DXGK\_ALLOCATIONGROUPOUT 構造体


DXGK\_ALLOCATIONGROUPOUT 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONGROUPOUT {
  UINT                           NbAllocationGroup;
  DXGK_ALLOCATIONGROUPDESCRIPTOR *pAllocationGroupDescriptor;
} DXGK_ALLOCATIONGROUPOUT;
```

<a name="members"></a>メンバー
-------

**NbAllocationGroup**システム用に予約されています。

**pAllocationGroupDescriptor**システム用に予約されています。

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

 

 





