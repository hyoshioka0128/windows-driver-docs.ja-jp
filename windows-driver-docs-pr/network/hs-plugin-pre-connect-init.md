---
title: HS_PLUGIN_PRE_CONNECT_INIT 関数
description: ホット スポット ネットワークへの接続が進行中の場合、その状態を初期化するためにプラグインを通知する HS_PLUGIN_PRE_CONNECT_INIT 関数と呼びます。
ms.assetid: 799242a0-144f-4d3f-b48c-9e96a851d8c4
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_PRE_CONNECT_INIT) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: a949921041a364e0f7f95f1f9558038d49c79816
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532105"
---
# <a name="hspluginpreconnectinit-function"></a>HS\_プラグイン\_PRE\_CONNECT\_INIT 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_PRE\_CONNECT\_INIT**にホット スポット ネットワークへの接続が進行中の場合、その状態を初期化するためにプラグインを通知する関数が呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_PRE_CONNECT_INIT)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>パラメーター
----------

*\*pNetworkIdentity* \[in\]  
ポインター、 [ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)ターゲット ネットワークの構造体。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

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


[**HS\_ネットワーク\_IDENTITY**](hs-network-identity.md)

 

 




