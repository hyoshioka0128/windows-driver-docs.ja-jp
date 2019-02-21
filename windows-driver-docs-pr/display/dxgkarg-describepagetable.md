---
title: '\_DXGKARG\_DESCRIBEPAGETABLE 構造体'
description: DXGKARG\_DESCRIBEPAGETABLE 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: f439ba7c-216e-4286-9a63-d8f596996ac2
keywords:
- _DXGKARG_DESCRIBEPAGETABLE 構造体のディスプレイ デバイス
- DXGKARG_DESCRIBEPAGETABLE 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_DESCRIBEPAGETABLE
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 21bdb72b5623c5cfbb4435983bb731a6ec7f5731
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557018"
---
# <a name="dxgkargdescribepagetable-structure"></a>\_DXGKARG\_DESCRIBEPAGETABLE 構造体


DXGKARG\_DESCRIBEPAGETABLE 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_DESCRIBEPAGETABLE {
  D3DGPU_VIRTUAL_ADDRESS CoverageStart;
  UINT                   CoverageSizeInBytes;
  UINT                   SizeInBytes;
  UINT                   SubtableOffset1;
  UINT                   SubtableOffset2;
} DXGKARG_DESCRIBEPAGETABLE;
```

<a name="members"></a>Members
-------

**CoverageStart**システム用に予約されています。

**CoverageSizeInBytes**システム用に予約されています。

**SizeInBytes**システム用に予約されています。

**SubtableOffset1**システム用に予約されています。

**SubtableOffset2**システム用に予約されています。

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

 

 





