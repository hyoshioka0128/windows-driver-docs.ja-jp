---
title: '\_DXGK\_ALLOCATIONGROUPDESCRIPTOR 構造体'
description: DXGK\_ALLOCATIONGROUPDESCRIPTOR 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 74ca560d-b5ec-40f1-a064-4972c7908fc9
keywords:
- _DXGK_ALLOCATIONGROUPDESCRIPTOR 構造体のディスプレイ デバイス
- DXGK_ALLOCATIONGROUPDESCRIPTOR 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_ALLOCATIONGROUPDESCRIPTOR
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f5b8c7149b7664b78fd4a20e20fde5d0f4be6c16
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558684"
---
# <a name="dxgkallocationgroupdescriptor-structure"></a>\_DXGK\_ALLOCATIONGROUPDESCRIPTOR 構造体


DXGK\_ALLOCATIONGROUPDESCRIPTOR 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_ALLOCATIONGROUPDESCRIPTOR {
  D3DGPU_VIRTUAL_ADDRESS MinimumVirtualAddress;
  D3DGPU_VIRTUAL_ADDRESS MaximumVirtualAddress;
} DXGK_ALLOCATIONGROUPDESCRIPTOR;
```

<a name="members"></a>Members
-------

**MinimumVirtualAddress**システム用に予約されています。

**MaximumVirtualAddress**システム用に予約されています。

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

 

 





