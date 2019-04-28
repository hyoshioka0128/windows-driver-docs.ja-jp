---
title: D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_範囲の構造体
description: システムの使用に予約されています。 ドライバーでは使用しないでください。この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dumddi.h ヘッダーでのみ使用できますに注意してください。 以降のバージョンのヘッダーから削除されました。 .
ms.assetid: 61393cb5-eedc-4186-a321-703b74450ee5
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c012dc263fde65fc9f23b2bb8438b0e2ee8752c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382963"
---
# <a name="d3dddimultiplaneoverlayfilterrange-structure"></a>D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルター\_範囲の構造体


システムの使用に予約されています。 ドライバーでは使用しないでください。

&gt; \[!注\]&gt;この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dumddi.h ヘッダーでのみ使用できます。 以降のバージョンのヘッダーから削除されました。

 

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE {
  INT   Minimum;
  INT   Maximum;
  INT   Default;
  FLOAT Multiplier;
} D3DDDI_MULTIPLANE_OVERLAY_FILTER_RANGE;
```

<a name="members"></a>メンバー
-------

**最小値**

**最大値**

**Default**

**乗数**

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
<td align="left">D3dumddi.h</td>
</tr>
</tbody>
</table>

 

 





