---
title: '\_DXGK\_VIRTUALADDRESSCAPS 構造体'
description: DXGK\_VIRTUALADDRESSCAPS 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 45a33031-26ca-4477-9be0-2066927506cf
keywords:
- _DXGK_VIRTUALADDRESSCAPS は、ディスプレイ デバイスを構成します。
- DXGK_VIRTUALADDRESSCAPS 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_VIRTUALADDRESSCAPS
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcba07e6797789f5251077f8f1023ef3ab909b6b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550376"
---
# <a name="dxgkvirtualaddresscaps-structure"></a>\_DXGK\_VIRTUALADDRESSCAPS 構造体


DXGK\_VIRTUALADDRESSCAPS 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_VIRTUALADDRESSCAPS {
  union {
    struct {
      UINT PrivilegedMemorySupported  :1;
      UINT ReadOnlyMemorySupported  :1;
      UINT Reserved  :30;
    };
    UINT Value;
  };
  UINT VirtualAddressBitCount;
  UINT PageTableCoverageBitCount;
  UINT PageDirectoryEntrySize;
  UINT PageDirectorySegment;
  UINT PageTableSegment;
  UINT IdealGPUPageSize;
} DXGK_VIRTUALADDRESSCAPS;
```

<a name="members"></a>Members
-------

**PrivilegedMemorySupported**システム用に予約されています。

**ReadOnlyMemorySupported**システム用に予約されています。

**予約済み**システム用に予約されています。

**値**システム用に予約されています。

**VirtualAddressBitCount**システム用に予約されています。

**PageTableCoverageBitCount**システム用に予約されています。

**PageDirectoryEntrySize**システム用に予約されています。

**PageDirectorySegment**システム用に予約されています。

**PageTableSegment**システム用に予約されています。

**IdealGPUPageSize**システム用に予約されています。

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

 

 





