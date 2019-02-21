---
title: '\_DXGK\_CREATEALLOCATIONFLAGS2 構造体'
description: DXGK\_CREATEALLOCATIONFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: c0d57a64-c509-4d72-81eb-7591bb0c1b9b
keywords:
- _DXGK_CREATEALLOCATIONFLAGS2 構造体のディスプレイ デバイス
- DXGK_CREATEALLOCATIONFLAGS2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_CREATEALLOCATIONFLAGS2
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: be2ec4413767a24b09ee9e7b880731a956e5b5d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539228"
---
# <a name="dxgkcreateallocationflags2-structure"></a>\_DXGK\_CREATEALLOCATIONFLAGS2 構造体


DXGK\_CREATEALLOCATIONFLAGS2 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_CREATEALLOCATIONFLAGS2 {
  union {
    struct {
      UINT Resource;
      UINT Reserved;
    };
    UINT Value;
  };
} DXGK_CREATEALLOCATIONFLAGS2;
```

<a name="members"></a>Members
-------

**リソース**システム用に予約されています。

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

 

 





