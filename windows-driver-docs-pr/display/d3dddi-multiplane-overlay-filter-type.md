---
title: D3DDDI \_ multiplane \_ オーバーレイ \_ フィルターの \_ 種類の列挙型
description: システムで使用するために予約されています。 ドライバーでは使用しないでください。注この構造は、windows 8 に付属している Windows Driver Kit (WDK) バージョン8で提供されている D3dumddi ヘッダーでのみ使用できます。 ヘッダーの新しいバージョンからは削除されています。.
ms.assetid: ceca0ed8-7d46-45e1-86cb-3d0506d26328
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE 列挙ディスプレイデバイス
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
ms.openlocfilehash: 718cfd5e6e6f0cfe54e50aebbc94a21758240877
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852131"
---
# <a name="d3dddi_multiplane_overlay_filter_type-enumeration"></a>D3DDDI \_ multiplane \_ オーバーレイ \_ フィルターの \_ 種類の列挙型


システムで使用するために予約されています。 ドライバーでは使用しないでください。

> [!NOTE]
> この構造は、windows 8 に付属している Windows Driver Kit (WDK) バージョン8で提供されている D3dumddi ヘッダーでのみ使用できます。 ヘッダーの新しいバージョンからは削除されています。

 

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

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_BRIGHTNESS"></span><span id="d3dddi_multiplane_overlay_filter_caps_brightness"></span>**D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター \_ キャップの \_ 明るさ**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_CONTRAST"></span><span id="d3dddi_multiplane_overlay_filter_caps_contrast"></span>**D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター \_ キャップの \_ コントラスト**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_HUE"></span><span id="d3dddi_multiplane_overlay_filter_caps_hue"></span>**D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター \_ キャップの \_ 色合い**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_SATURATION"></span><span id="d3dddi_multiplane_overlay_filter_caps_saturation"></span>**D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター \_ キャップの \_ 彩度**

<span id="D3DDDI_MULTIPLANE_OVERLAY_FILTER_CAPS_STRETCH_QUALITY"></span><span id="d3dddi_multiplane_overlay_filter_caps_stretch_quality"></span>**D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター \_ キャップの \_ ストレッチ \_ 品質**

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
<td align="left"><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">D3dumddi</td>
</tr>
</tbody>
</table>

 

 





