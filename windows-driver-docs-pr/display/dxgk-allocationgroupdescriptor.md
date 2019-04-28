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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372982"
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

<a name="members"></a>メンバー
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

 

 





