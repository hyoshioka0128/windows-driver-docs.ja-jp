---
title: D3DKMT\_MULTIPLANE\_オーバーレイ\_属性の構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 07abf207-62ab-42d1-84b0-74815d1d42b8
keywords:
- D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES
api_location:
- D3dkmthk.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 392b40acbda1732a860c5918685e4b2f016df2ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558024"
---
# <a name="d3dkmtmultiplaneoverlayattributes-structure"></a>D3DKMT\_MULTIPLANE\_オーバーレイ\_属性の構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES {
  UINT                                         Flags;
  RECT                                         SrcRect;
  RECT                                         DstRect;
#if (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM1_3)
  RECT                                         ClipRect;
#endif
  D3DDDI_ROTATION                              Rotation;
  D3DKMT_MULTIPLANE_OVERLAY_BLEND              Blend;
#if (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM1_3)
  UINT                                         DirtyRectCount;
  RECT                                         pDirtyRects;
#else
  UINT                                         NumFilters;
  void                                         *pFilters;
#endif
  D3DKMT_MULTIPLANE_OVERLAY_VIDEO_FRAME_FORMAT VideoFrameFormat;
  UINT                                         YCbCrFlags;
  D3DKMT_MULTIPLANE_OVERLAY_STEREO_FORMAT      StereoFormat;
  BOOL                                         StereoLeftViewFrame0;
  BOOL                                         StereoBaseViewFrame0;
  DXGKMT_MULTIPLANE_OVERLAY_STEREO_FLIP_MODE   StereoFlipMode;
#if (DXGKDDI_INTERFACE_VERSION >= DXGKDDI_INTERFACE_VERSION_WDDM1_3)
  DXGKMT_MULTIPLANE_OVERLAY_STRETCH_QUALITY    StretchQuality;
#endif
} D3DKMT_MULTIPLANE_OVERLAY_ATTRIBUTES;
```

<a name="members"></a>Members
-------

**フラグ**

**SrcRect**

**DstRect**

**ClipRect**

**回転**

**blend**

**DirtyRectCount**

**pDirtyRects**

**NumFilters**

**pFilters**

**VideoFrameFormat**

**YCbCrFlags**

**StereoFormat**

**StereoLeftViewFrame0**

**StereoBaseViewFrame0**

**StereoFlipMode**

**StretchQuality**

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
<td align="left">D3dkmthk.h</td>
</tr>
</tbody>
</table>

 

 





