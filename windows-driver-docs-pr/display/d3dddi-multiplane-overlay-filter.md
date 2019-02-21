---
title: D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルターの構造
description: システムの使用に予約されています。 ドライバーでは使用しないでください。この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dumddi.h ヘッダーでのみ使用できますに注意してください。 以降のバージョンのヘッダーから削除されました。 .
ms.assetid: 56276b78-5550-4d93-8a73-b1183deb54da
keywords:
- D3DDDI_MULTIPLANE_OVERLAY_FILTER 構造体のディスプレイ デバイス
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
ms.openlocfilehash: e166be1415c6b129fedcc5b8165634bbe5133b38
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536056"
---
# <a name="d3dddimultiplaneoverlayfilter-structure"></a>D3DDDI\_MULTIPLANE\_オーバーレイ\_フィルターの構造


システムの使用に予約されています。 ドライバーでは使用しないでください。

&gt; \[!注\]&gt;この構造体は Windows Driver Kit (WDK) 8 付属するバージョンの Windows 8 で提供される D3dumddi.h ヘッダーでのみ使用できます。 以降のバージョンのヘッダーから削除されました。

 

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _D3DDDI_MULITPLANE_OVERLAY_FILTER {
  D3DDDI_MULTIPLANE_OVERLAY_FILTER_TYPE FilterType;
  BOOL                                  Enabled;
  INT                                   Value;
} D3DDDI_MULTIPLANE_OVERLAY_FILTER;
```

<a name="members"></a>Members
-------

**filterType**

**有効になっています。**

**値**

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

 

 





