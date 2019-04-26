---
title: D3DKMT\_OUTPUTDUPL\_メタデータ構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: abf4f00a-05bb-48f6-989e-f1b453fb0708
keywords:
- D3DKMT_OUTPUTDUPL_METADATA 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_METADATA
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: df6a9b410a7498c3aadc31a68435af08c19b9836
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346235"
---
# <a name="d3dkmtoutputduplmetadata-structure"></a>D3DKMT\_OUTPUTDUPL\_メタデータ構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_METADATA {
  D3DKMT_HANDLE                  hAdapter;
  D3DDDI_VIDEO_PRESENT_SOURCE_ID VidPnSourceId;
  D3DKMT_OUTPUTDUPL_METADATATYPE Type;
  UINT                           BufferSizeSupplied;
  PVOID                          pBuffer;
  UINT                           BufferSizeRequired;
} D3DKMT_OUTPUTDUPL_METADATA;
```

<a name="members"></a>メンバー
-------

**hAdapter**

**VidPnSourceId**

**型**

**BufferSizeSupplied**

**pBuffer**

**BufferSizeRequired**

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

 

 





