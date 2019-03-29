---
title: DXGK\_SEGMENTFLAGS2 構造体
description: DXGK\_SEGMENTFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 9e6f96a2-d32f-4ef8-aaad-dc0cbd053222
keywords:
- DXGK_SEGMENTFLAGS2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_SEGMENTFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a403faf9a775b7b40a142fe973dd3e96bdc2adbf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577719"
---
# <a name="dxgksegmentflags2-structure"></a>DXGK\_SEGMENTFLAGS2 構造体


DXGK\_SEGMENTFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_SEGMENTFLAGS2 {
  union {
    struct {
      UINT Aperture  :1;
      UINT PopulatedFromSystemMemory  :1;
      UINT SystemMemoryReservedByBios  :1;
      UINT CpuVisible  :1;
      UINT Reserved  :28;
    };
    UINT Value;
  };
} DXGK_SEGMENTFLAGS2;
```

<a name="members"></a>メンバー
-------

**Aperture**システム用に予約されています。

**PopulatedFromSystemMemory**システム用に予約されています。

**SystemMemoryReservedByBios**システム用に予約されています。

**CpuVisible**システム用に予約されています。

**予約済み**システム用に予約されています。

**値**システム用に予約されています。

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

 

 





