---
title: HS_PLUGIN_VERSION 構造体
description: HS_PLUGIN_VERSION 構造体には、プラグインがサポートされている最小値と最大のホット スポット ホスト バージョンが含まれています。
ms.assetid: ced24606-0379-4b13-831c-11de3ed6cd2b
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_PLUGIN_VERSION 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_PLUGIN_VERSION 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db1c982afe60fbaa492b551fa452aede38370c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580058"
---
# <a name="hspluginversion-structure"></a>HS\_プラグイン\_バージョン構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_バージョン**構造体には、プラグインによってサポートされている最小値と最大のホット スポット ホスト バージョンが含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_VERSION {
  DWORD dwVerMin;
  DWORD dwVerMax;
} HS_PLUGIN_VERSION, *PHS_PLUGIN_VERSION;
```

<a name="members"></a>メンバー
-------

**dwVerMin**  
プラグインがサポートされている最小のホット スポット ホスト バージョンです。

**dwVerMax**  
プラグインがサポートされている最大のホット スポット ホスト バージョンです。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

 

 




