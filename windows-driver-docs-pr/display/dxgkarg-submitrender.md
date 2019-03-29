---
title: '\_DXGKARG\_SUBMITRENDER 構造体'
description: DXGKARG\_SUBMITRENDER 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: eecc3c47-1387-4fca-9113-12dfedc58e80
keywords:
- _DXGKARG_SUBMITRENDER 構造体のディスプレイ デバイス
- DXGKARG_SUBMITRENDER 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGKARG_SUBMITRENDER
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 15032e403895e5cf45a3e656f5caf15e000cfc89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570855"
---
# <a name="dxgkargsubmitrender-structure"></a>\_DXGKARG\_SUBMITRENDER 構造体


DXGKARG\_SUBMITRENDER 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGKARG_SUBMITRENDER {
  VOID                   *pContextSaveArea;
  D3DGPU_VIRTUAL_ADDRESS DmaBuffer;
  UINT                   DmaSize;
  VOID                   *pPrivateDriverData;
  UINT                   PrivateDriverDataSize;
  VOID                   *pDmaBufferPrivateData;
  UINT                   DmaBufferPrivateDataSize;
  VOID                   *pDmaBuffer;
} DXGKARG_SUBMITRENDER;
```

<a name="members"></a>メンバー
-------

**pContextSaveArea**システム用に予約されています。

**DmaBuffer**システム用に予約されています。

**DmaSize**システム用に予約されています。

**pPrivateDriverData**システム用に予約されています。

**PrivateDriverDataSize**システム用に予約されています。

**pDmaBufferPrivateData**システム用に予約されています。

**DmaBufferPrivateDataSize**システム用に予約されています。

**pDmaBuffer**システム用に予約されています。

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

 

 





