---
title: D3DKMT\_OUTPUTDUPL\_FRAMEINFO 構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: e35389b2-52aa-4481-a5d7-6c45c795885f
keywords:
- D3DKMT_OUTPUTDUPL_FRAMEINFO 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_OUTPUTDUPL_FRAMEINFO
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 31932a1d3da957249e64552f17d86ad5df714971
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578019"
---
# <a name="d3dkmtoutputduplframeinfo-structure"></a>D3DKMT\_OUTPUTDUPL\_FRAMEINFO 構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DKMT_OUTPUTDUPL_FRAMEINFO {
  LARGE_INTEGER                      LastPresentTime;
  LARGE_INTEGER                      LastMouseUpdateTime;
  UINT                               AccumulatedFrames;
  BOOL                               RectsCoalesced;
  BOOL                               ProtectedContentMaskedOut;
  D3DKMT_OUTPUTDUPL_POINTER_POSITION PointerPosition;
  UINT                               TotalMetadataBufferSize;
  UINT                               PointerShapeBufferSize;
} D3DKMT_OUTPUTDUPL_FRAMEINFO;
```

<a name="members"></a>メンバー
-------

**LastPresentTime**

**LastMouseUpdateTime**

**AccumulatedFrames**

**RectsCoalesced**

**ProtectedContentMaskedOut**

**PointerPosition**

**TotalMetadataBufferSize**

**PointerShapeBufferSize**

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

 

 





