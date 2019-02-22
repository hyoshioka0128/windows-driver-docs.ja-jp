---
title: HS_PLUGIN_HOST_NAME 構造体
description: HS_PLUGIN_HOST_NAME 構造体には、ホスト名が含まれています。
ms.assetid: 3995fff6-6992-4dd6-a94c-a27b2ee44436
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_PLUGIN_HOST_NAME 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_PLUGIN_HOST_NAME 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4457f8f594fe1a2663c23929e045865ba92ed18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552703"
---
# <a name="hspluginhostname-structure"></a>HS\_プラグイン\_ホスト\_名の構造

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_ホスト\_名前**構造体には、ホスト名が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_PLUGIN_HOST_NAME {
  WHCAR pszHostName[HS_CONST_MAX_HOST_NAME_LENGTH+1];
} HS_PLUGIN_HOST_NAME, *PHS_PLUGIN_HOST_NAME;
```

<a name="members"></a>Members
-------

**pszHostName**  
ホスト名へのポインター。

<a name="requirements"></a>要件
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

 

 




