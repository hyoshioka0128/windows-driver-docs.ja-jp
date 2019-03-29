---
title: D3DKMT\_SCATTERBLTS 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: a5ce5557-840c-4044-92d8-7e38c592c747
keywords:
- D3DKMT_SCATTERBLTS 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_SCATTERBLTS
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: abc0e5cb7300123bf453889ea85f80204679450e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582582"
---
# <a name="d3dkmtscatterblts-structure"></a>D3DKMT\_SCATTERBLTS 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_SCATTERBLTS {
  UINT              NumBlts;
  D3DKMT_SCATTERBLT Blts[D3DKMT_MAX_PRESENT_HISTORY_SCATTERBLTS];
} D3DKMT_SCATTERBLTS;
```

<a name="members"></a>メンバー
-------

**NumBlts**

**Blt**

<a name="requirements"></a>必要条件
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

 

 





