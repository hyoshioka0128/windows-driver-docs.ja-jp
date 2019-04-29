---
title: HSPluginGetVersion 関数
description: HSPluginGetVersion 関数では、プラグイン DLL によってエクスポートし、プラグインのバージョンが、ホストのバージョンと一致することを確認するために呼び出されます。
ms.assetid: dfdd534c-43c0-4d96-b85b-de9c2830322d
keywords:
- Windows Vista 以降のドライバーをネットワーク HSPluginGetVersion 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1a3709b96a2584e44942be540949fad8a09b3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322140"
---
# <a name="hsplugingetversion-function"></a>HSPluginGetVersion 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HSPluginGetVersion**関数がプラグイン DLL からエクスポートされ、プラグインのバージョンが、ホストのバージョンと一致することを確認すると呼びます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
DWORD HSPluginGetVersion(
  _Out_ HS_PLUGIN_VERSION *pHotspotPluginVersion
);
```

<a name="parameters"></a>パラメーター
----------

*\*pHotspotPluginVersion* \[out\]  
ポインター、 [ **HS\_プラグイン\_バージョン**](hs-plugin-version.md)プラグインのバージョン情報を含む構造体。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**HS\_プラグイン\_バージョン**](hs-plugin-version.md)

 

 




