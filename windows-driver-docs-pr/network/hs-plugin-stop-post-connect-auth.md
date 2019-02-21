---
title: HS_PLUGIN_STOP_POST_CONNECT_AUTH 関数
description: 認証プロセスを停止するプラグインに通知する HS_PLUGIN_STOP_POST_CONNECT_AUTH 関数と呼びます。
ms.assetid: 2e4e01b1-e41a-41db-a3ca-6cc6b53b3a8b
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_STOP_POST_CONNECT_AUTH) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe1b3d25b236a1ae7a6afe43b30d3f9270b24649
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528748"
---
# <a name="hspluginstoppostconnectauth-function"></a>HS\_プラグイン\_停止\_POST\_CONNECT\_AUTH 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_停止\_POST\_CONNECT\_AUTH**認証プロセスを停止するプラグインに通知する関数が呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_STOP_POST_CONNECT_AUTH)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>パラメーター
----------

*\*pNetworkIdentity* \[in\]  
[ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)ネットワークを一意に識別する構造体。

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

 

 




