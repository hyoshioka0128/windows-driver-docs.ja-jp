---
title: HS_PLUGIN_IS_HOTSPOT_NETWORK 関数
description: HS_PLUGIN_IS_HOTSPOT_NETWORK 関数は、指定されたネットワークがホット スポット ネットワークかどうかを決定ホストによって呼び出されます。
ms.assetid: 24a26ee0-9eb1-49fa-95da-40315a4aab3a
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_IS_HOTSPOT_NETWORK) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52bd0fefd29dc2aafeba7c3484f7fab6237da18b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322290"
---
# <a name="hspluginishotspotnetwork-function"></a>HS\_プラグイン\_IS\_ホット スポット\_ネットワーク関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_IS\_ホット スポット\_ネットワーク**関数は指定されたネットワークがホット スポット ネットワークかどうかを決定ホストによって呼び出されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_IS_HOTSPOT_NETWORK)(
  _In_      HS_NETWORK_IDENTITY *pNetworkIdentity,
  _Out_     eHS_NETWORK_STATE   *pNetworkState,
  _Out_opt_ HS_NETWORK_PROFILE  *pNetworkProfile
);
```

<a name="parameters"></a>パラメーター
----------

*\*pNetworkIdentity* \[in\]  
ポインター、 [ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)デバイスを切断する元となるネットワークの構造体。

*\*pNetworkState* \[out\]  
[ **EHS\_ネットワーク\_状態**](ehs-network-state.md)ネットワークの種類を示す列挙値。

*\*pNetworkProfile* \[アウト、省略可能\]  
ポインター、 [ **HS\_ネットワーク\_プロファイル**](hs-network-profile.md)ネットワークの構造体。

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

[**eHS\_ネットワーク\_状態**](ehs-network-state.md)

[**HS\_ネットワーク\_プロファイル**](hs-network-profile.md)

 

 




