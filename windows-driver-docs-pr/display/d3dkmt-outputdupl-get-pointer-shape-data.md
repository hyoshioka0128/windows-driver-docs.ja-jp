---
title: D3DKMT\_OUTPUTDUPL\_取得\_ポインター\_図形\_データ構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 31502888-88b0-49c2-8f03-63bb31886931
keywords:
- D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4ef1b97c96339ed747f8dac108230f325fa606c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346245"
---
# <a name="d3dkmtoutputduplgetpointershapedata-structure"></a>D3DKMT\_OUTPUTDUPL\_取得\_ポインター\_図形\_データ構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA {
  D3DKMT_HANDLE                     hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID    VidPnSourceId;
  UINT                              BufferSizeSupplied;
  PVOID                             pShapeBuffer;
  UINT                              BufferSizeRequired;
  D3DKMT_OUTDUPL_POINTER_SHAPE_INFO ShapeInfo;
} D3DKMT_OUTPUTDUPL_GET_POINTER_SHAPE_DATA;
```

<a name="members"></a>メンバー
-------

**hAdapter**

**VidPnSourceId**

**BufferSizeSupplied**

**pShapeBuffer**

**BufferSizeRequired**

**ShapeInfo**

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

 

 





