---
title: D3DKMT\_OUTDUPL\_ポインター\_図形\_情報構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: fc72fe82-8807-44ac-b9da-8f84d38c45bf
keywords:
- D3DKMT_OUTDUPL_POINTER_SHAPE_INFO 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_OUTDUPL_POINTER_SHAPE_INFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b9d13dfbcd76612c2de97d8c1b4f104e64efa40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552641"
---
# <a name="d3dkmtoutduplpointershapeinfo-structure"></a>D3DKMT\_OUTDUPL\_ポインター\_図形\_情報構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTDUPL_POINTER_SHAPE_INFO {
  D3DKMT_OUTDUPL_POINTER_SHAPE_TYPE Type;
  UINT                              Width;
  UINT                              Height;
  UINT                              Pitch;
  POINT                             HotSpot;
} D3DKMT_OUTDUPL_POINTER_SHAPE_INFO;
```

<a name="members"></a>Members
-------

**型**

**幅**

**高さ**

**ピッチ**

**ホット スポット**

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dkmthk.h (D3dkmthk.h を含む)</td>
</tr>
</tbody>
</table>

 

 





