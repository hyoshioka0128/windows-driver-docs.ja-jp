---
title: DXGK\_QUERYSEGMENTOUT2 構造体
description: DXGK\_QUERYSEGMENTOUT2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 7193c763-fd76-4d7a-81ac-dfcc2b7bf881
keywords:
- DXGK_QUERYSEGMENTOUT2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_QUERYSEGMENTOUT2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c24a6c657c25b27518888ac53d6114bf663707a8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392033"
---
# <a name="dxgkquerysegmentout2-structure"></a>DXGK\_QUERYSEGMENTOUT2 構造体


DXGK\_QUERYSEGMENTOUT2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_QUERYSEGMENTOUT2 {
  UINT                    SegmentCount;
  DXGK_SEGMENTDESCRIPTOR2 *pSegmentDescriptor;
} DXGK_QUERYSEGMENTOUT2;
```

<a name="members"></a>メンバー
-------

**SegmentCount**システム用に予約されています。

**pSegmentDescriptor**システム用に予約されています。

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

 

 





