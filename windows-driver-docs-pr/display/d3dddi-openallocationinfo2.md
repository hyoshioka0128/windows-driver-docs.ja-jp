---
title: D3DDDI\_OPENALLOCATIONINFO2 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 5C439C23-75B1-422C-850D-6980CC89539B
keywords:
- D3DDDI_OPENALLOCATIONINFO2 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DDDI_OPENALLOCATIONINFO2
api_location:
- D3dukmdt.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 62709710baab35ac23cd373343db9b95f27a7003
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556707"
---
# <a name="d3dddiopenallocationinfo2-structure"></a>D3DDDI\_OPENALLOCATIONINFO2 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DDDI_OPENALLOCATIONINFO2 {
  D3DKMT_HANDLE          hAllocation;
  const VOID             *pPrivateDriverData;
  UINT                   PrivateDriverDataSize;
  D3DGPU_VIRTUAL_ADDRESS GpuVirtualAddress;
  ULONG_PTR              Reserved[6];
} D3DDDI_OPENALLOCATIONINFO2;
```

<a name="members"></a>Members
-------

**hAllocation**

**pPrivateDriverData**

**PrivateDriverDataSize**

**GpuVirtualAddress**

**予約されています**

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
<td align="left"><p>Windows 7</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dukmdt.h (D3dukmdt.h または D3dkmddi.h を含む)</td>
</tr>
</tbody>
</table>

 

 





