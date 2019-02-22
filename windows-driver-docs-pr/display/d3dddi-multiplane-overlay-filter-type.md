---
title: D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_種類の列挙型
description: システムの使用に予約されています。 ドライバーでは使用しないでください。この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dumddi.h ヘッダーでのみ使用できますに注意してください。 以降のバージョンのヘッダーから削除されました。 .
ms.assetid: ceca0ed8-7d46-45e1-86cb-3d0506d26328
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE 列挙ディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4dbbedd2128f5627539b9ad4f27ab9f896aa3294
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559810"
---
# <a name="d3dddimultiplaneoverlayfiltertype-enumeration"></a>D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_種類の列挙型


システムの使用に予約されています。 ドライバーでは使用しないでください。

&gt; \[!注\]&gt;この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dumddi.h ヘッダーでのみ使用できます。 以降のバージョンのヘッダーから削除されました。

 

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE {
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_BRIGHTNESS       = 0x1,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_CONTRAST         = 0x2,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_HUE              = 0x4,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_SATURATION       = 0x8,
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_STRETCH_QUALITY  = 0x10
} D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE;
```

<a name="constants"></a>定数
---------

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_BRIGHTNESS"></span><span id="d3dddi_multiplane_overlay_filter_caps_brightness"></span>**D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_CAP\_明るさ**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_CONTRAST"></span><span id="d3dddi_multiplane_overlay_filter_caps_contrast"></span>**D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_CAP\_コントラスト**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_HUE"></span><span id="d3dddi_multiplane_overlay_filter_caps_hue"></span>**D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_CAP\_HUE**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_SATURATION"></span><span id="d3dddi_multiplane_overlay_filter_caps_saturation"></span>**D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_CAP\_彩度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_STRETCH_QUALITY"></span><span id="d3dddi_multiplane_overlay_filter_caps_stretch_quality"></span>**D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_CAP\_STRETCH\_品質**

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
<td align="left">D3dumddi.h</td>
</tr>
</tbody>
</table>

 

 





