---
title: '\_DXGK\_MULTIPLANE\_オーバーレイ\_フィルターの構造'
description: システムの使用に予約されています。 ドライバーでは使用しないでください。この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dkmddi.h ヘッダーでのみ使用できますに注意してください。 以降のバージョンのヘッダーから削除されました。 .
ms.assetid: db369274-df58-40b0-8f2c-c1963dfa3607
keywords:
- _DXGK_MULTIPLANE_OVERLAY_FILTER 構造体のディスプレイ デバイス
- DXGK_MULTIPLANE_OVERLAY_FILTER 構造体のディスプレイ デバイス
topic_type:
- apiref
api_name:
- DXGK_MULTIPLANE_OVERLAY_FILTER
api_location:
- D3dkmddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c242686c494b3d62813b0a6a19ffdfceea760f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350306"
---
# <a name="dxgkmultiplaneoverlayfilter-structure"></a>\_DXGK\_MULTIPLANE\_オーバーレイ\_フィルターの構造


システムの使用に予約されています。 ドライバーでは使用しないでください。

&gt; \[!注\]&gt;この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dkmddi.h ヘッダーでのみ使用できます。 以降のバージョンのヘッダーから削除されました。

 

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _DXGK_MULITPLANE_OVERLAY_FILTER {
  DXGK_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                Enabled;
  INT                                 Value;
} DXGK_MULTIPLANE_OVERLAY_FILTER;
```

<a name="members"></a>メンバー
-------

**filterType**

**有効**

**値**

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
<td align="left">D3dkmddi.h</td>
</tr>
</tbody>
</table>

 

 





