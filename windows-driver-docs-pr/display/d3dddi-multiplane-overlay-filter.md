---
title: D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター構造
description: システムで使用するために予約されています。 ドライバーでは使用しないでください。注この構造は、windows 8 に付属している Windows Driver Kit (WDK) バージョン8で提供されている D3dumddi ヘッダーでのみ使用できます。 ヘッダーの新しいバージョンからは削除されています。.
ms.assetid: 56276b78-5550-4d93-8a73-b1183deb54da
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER 構造の表示デバイス
topic_type:
- apiref
api_name:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER
api_location:
- D3dumddi.h
api_type:
- HeaderDef
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5dcd273bd01dae78f5a40161470b710d61109d1a
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852129"
---
# <a name="d3dddi_multiplane_overlay_filter-structure"></a>D3DDDI \_ multiplane \_ オーバーレイ \_ フィルター構造


システムで使用するために予約されています。 ドライバーでは使用しないでください。

> [!NOTE]
> この構造は、windows 8 に付属している Windows Driver Kit (WDK) バージョン8で提供されている D3dumddi ヘッダーでのみ使用できます。 ヘッダーの新しいバージョンからは削除されています。

 

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DDDI_MULITPLANE_OVERLAY_FILTER {
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                  Enabled;
  INT                                   Value;
} D3DDDI_MULTIPLANE_OVERLAY_FILTER;
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
<td align="left">D3dumddi</td>
</tr>
</tbody>
</table>

 

 





