---
title: DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP 列挙型
description: システムの使用に予約されています。 ドライバーでは使用しないでください。
ms.assetid: 28017595-06d5-48ff-91d7-0e084d1e92de
keywords:
- DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS 列挙ディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS
api_location:
- Dxgiddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: a69ab7c28e10e17e98e8f75699ee1e9f58aa2c43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536536"
---
# <a name="dxgiddimultiplaneoverlaystereocaps-enumeration"></a>DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP 列挙型


システムの使用に予約されています。 ドライバーでは使用しないでください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS {
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_SEPARATE            = 0x1,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_ROW_INTERLEAVED     = 0x4,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_COLUMN_INTERLEAVED  = 0x8,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_CHECKERBOARD        = 0x10,
  DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_FLIP_MODE           = 0x20
} DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS;
```

<a name="constants"></a>定数
---------

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_SEPARATE"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_separate"></span>**DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP\_別**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_ROW_INTERLEAVED"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_row_interleaved"></span>**DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP\_行\_インターリーブ**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_COLUMN_INTERLEAVED"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_column_interleaved"></span>**DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP\_列\_インターリーブ**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_CHECKERBOARD"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_checkerboard"></span>**DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP\_チェッカー ボード**

<span id="DXGI_DDI_MULTIPLANE_OVERLAY_STEREO_CAPS_FLIP_MODE"></span><span id="dxgi_ddi_multiplane_overlay_stereo_caps_flip_mode"></span>**DXGI\_DDI\_MULTIPLANE\_オーバーレイ\_ステレオ\_CAP\_反転\_モード**

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
<td align="left">Dxgiddi.h</td>
</tr>
</tbody>
</table>

 

 





