---
title: D3DKMT\_TDRDBGCTRL\_エスケープ構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: dcb558ed-8072-4454-8aea-d966a65b5d63
keywords:
- D3DKMT_TDRDBGCTRL_ESCAPE 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_TDRDBGCTRL_ESCAPE
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f74f3b03f0573d6d42199606d4abb49887d96881
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530206"
---
# <a name="d3dkmttdrdbgctrlescape-structure"></a>D3DKMT\_TDRDBGCTRL\_エスケープ構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_TDRDBGCTRL_ESCAPE {
  D3DKMT_TDRDBGCTRLTYPE TdrControl;
  union {
    ULONG NodeOrdinal;
  };
} D3DKMT_TDRDBGCTRL_ESCAPE;
```

<a name="members"></a>Members
-------

**TdrControl**

**NodeOrdinal**

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

 

 





