---
title: '\_DXGK \_ multiplane \_ オーバーレイ \_ フィルター構造'
description: システムで使用するために予約されています。 ドライバーでは使用しないでください。注この構造は、windows 8 に付属している Windows Driver Kit (WDK) バージョン8で提供されている D3dkmddi ヘッダーでのみ使用できます。 ヘッダーの新しいバージョンからは削除されています。.
ms.assetid: db369274-df58-40b0-8f2c-c1963dfa3607
keywords:
- _DXGK_MULTIPLANE_OVERLAY_FILTER 構造の表示デバイス
- DXGK_MULTIPLANE_OVERLAY_FILTER 構造の表示デバイス
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
ms.openlocfilehash: 93b6148246a304670f97ef5df6886637535a9d91
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851733"
---
# <a name="_dxgk_multiplane_overlay_filter-structure"></a>\_DXGK \_ multiplane \_ オーバーレイ \_ フィルター構造


システムで使用するために予約されています。 ドライバーでは使用しないでください。

> [!NOTE]
>  この構造は、windows 8 に付属している Windows Driver Kit (WDK) バージョン8で提供されている D3dkmddi ヘッダーでのみ使用できます。 ヘッダーの新しいバージョンからは削除されています。

 

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

**FilterType**

**Enabled**

**Value**

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
<td align="left">D3dkmddi</td>
</tr>
</tbody>
</table>

 

 





