---
title: '\_DXGK\_DMABUFFERCAPS 構造体'
description: DXGK\_DMABUFFERCAPS 構造はシステム用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 57ccc0e6-eacf-48a2-a9a1-cb7e43850caa
keywords:
- _DXGK_DMABUFFERCAPS は、ディスプレイ デバイスを構成します。
- DXGK_DMABUFFERCAPS 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_DMABUFFERCAPS
api_location:
- d3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4caf3c18a133580b5479219b25897a09f374fdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327111"
---
# <a name="dxgkdmabuffercaps-structure"></a>\_DXGK\_DMABUFFERCAPS 構造体


DXGK\_DMABUFFERCAPS 構造はシステム用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_DMABUFFERCAPS {
  struct {
    UINT Size;
    UINT PrivateDriverDataSize;
    UINT SegmentId;
    UINT AllocationGroup;
    UINT Reserved[16];
  } PresentDmaBuffer;
  struct {
    UINT Size;
    UINT PrivateDriverDataSize;
    UINT SegmentId;
    UINT AllocationGroup;
    UINT Reserved[16];
  } PagingDmaBuffer;
} DXGK_DMABUFFERCAPS;
```

<a name="members"></a>メンバー
-------

**PresentDmaBuffer**

**PagingDmaBuffer**

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

 

 





