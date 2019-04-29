---
title: HS_PLUGIN_RESET 関数
description: HS_PLUGIN_RESET 関数は、その状態をリセットする必要がありますが、プラグインを通知するホストによって呼び出されます。
ms.assetid: 9f5683c9-b426-4802-85bd-c1ce770b9e46
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_RESET) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27795a01e46b0ee81ef0ef6554c14beec4080acc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322171"
---
# <a name="hspluginreset-function"></a>HS\_プラグイン\_RESET 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_リセット**の状態をリセットする必要がありますが、プラグインを通知するホストによって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_RESET)(
    
);
```

<a name="parameters"></a>パラメーター
----------

この関数には、パラメーターがありません。

**   

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

プラグインは、すべてのスレッドを終了し、進行中のすべてのアクティビティを停止する必要があります。

リセットに失敗した場合、このプラグインはアンロードされます。

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

 

 




