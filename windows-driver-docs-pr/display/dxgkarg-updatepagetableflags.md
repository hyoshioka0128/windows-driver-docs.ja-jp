---
title: '\_DXGKARG\_UPDATEPAGETABLEFLAGS 構造体'
description: DXGKARG\_UPDATEPAGETABLEFLAGS 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 59a3fb51-ba3e-420e-abf7-c3faacc25ebc
keywords:
- _DXGKARG_UPDATEPAGETABLEFLAGS は、ディスプレイ デバイスを構成します。
- DXGKARG_UPDATEPAGETABLEFLAGS 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_UPDATEPAGETABLEFLAGS
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6370ee8b5f683871ce957c889cc3e240edf56fc3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552545"
---
# <a name="dxgkargupdatepagetableflags-structure"></a>\_DXGKARG\_UPDATEPAGETABLEFLAGS 構造体


DXGKARG\_UPDATEPAGETABLEFLAGS 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_UPDATEPAGETABLEFLAGS {
  union {
    struct {
      UINT LinearAccess  :1;
      UINT Reserved  :31;
    };
    UINT Value;
  };
} DXGKARG_UPDATEPAGETABLEFLAGS;
```

<a name="members"></a>Members
-------

**LinearAccess**システム用に予約されています。

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

 

 





