---
title: D3DKMT\_SCATTERBLT 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 94463e11-8a18-4d23-b7b6-d2486dc7dc9d
keywords:
- D3DKMT_SCATTERBLT 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_SCATTERBLT
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 686d7444d69872df34d30984cfba3ac869d4f5be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557872"
---
# <a name="d3dkmtscatterblt-structure"></a>D3DKMT\_SCATTERBLT 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_SCATTERBLT {
  ULONG64 hLogicalSurfaceDestination;
  LONG64  hDestinationCompSurfDWM;
  UINT64  DestinationCompositionBindingId;
  RECT    SourceRect;
  POINT   DestinationOffset;
} D3DKMT_SCATTERBLT;
```

<a name="members"></a>Members
-------

**hLogicalSurfaceDestination**

**hDestinationCompSurfDWM**

**DestinationCompositionBindingId**

**SourceRect**

**DestinationOffset**

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

 

 





