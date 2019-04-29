---
title: '\_DXGK\_PDE 構造体'
description: DXGK\_PDE 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: e2cd4541-beda-4c61-bdba-a86ae3888501
keywords:
- _DXGK_PDE 構造体のディスプレイ デバイス
- DXGK_PDE 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_PDE
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b78cf2ade71e885665748cedbf9cd69e6ad8101
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392038"
---
# <a name="dxgkpde-structure"></a>\_DXGK\_PDE 構造体


DXGK\_PDE 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_PDE {
  union {
    struct {
      ULONGLONG Valid  :1;
      ULONGLONG Segment  :5;
      ULONGLONG Reserved  :6;
      ULONGLONG PageTableAddress  :52;
    };
    ULONGLONG Value;
  };
  UINT PageTableSizeInPages;
} DXGK_PDE;
```

<a name="members"></a>メンバー
-------

**有効な**システム用に予約されています。

**セグメント**システム用に予約されています。

**予約済み**システム用に予約されています。

**PageTableAddress**システム用に予約されています。

**値**システム用に予約されています。

**PageTableSizeInPages**システム用に予約されています。

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

 

 





