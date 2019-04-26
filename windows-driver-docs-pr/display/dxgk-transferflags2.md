---
title: '\_DXGK\_TRANSFERFLAGS2 構造体'
description: DXGK\_TRANSFERFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 5bc690c4-d95a-4048-b716-fb2b12a22a86
keywords:
- _DXGK_TRANSFERFLAGS2 構造体のディスプレイ デバイス
- DXGK_TRANSFERFLAGS2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_TRANSFERFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f017aaafc25f3e5acad42d84bb0a12ac42f1da75
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350284"
---
# <a name="dxgktransferflags2-structure"></a>\_DXGK\_TRANSFERFLAGS2 構造体


DXGK\_TRANSFERFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_TRANSFERFLAGS2 {
  union {
    struct {
      UINT Swizzle  :1;
      UINT Unswizzle  :1;
      UINT AllocationIsIdle  :1;
      UINT SwizzlingRange  :1;
      UINT Reserved  :28;
    };
    UINT Value;
  };
} DXGK_TRANSFERFLAGS2;
```

<a name="members"></a>メンバー
-------

**スィズル**システム用に予約されています。

**すべて**システム用に予約されています。

**AllocationIsIdle**システム用に予約されています。

**SwizzlingRange**システム用に予約されています。

**予約済み**システム用に予約されています。

**値**システム用に予約されています。

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

 

 





