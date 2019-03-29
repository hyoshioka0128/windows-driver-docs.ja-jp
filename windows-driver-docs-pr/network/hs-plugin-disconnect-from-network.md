---
title: HS_PLUGIN_DISCONNECT_FROM_NETWORK 関数
description: HS_PLUGIN_DISCONNECT_FROM_NETWORK 関数では、デバイスをネットワークから切断すること、プラグインを通知します。
ms.assetid: 8a53c824-18f7-4000-b264-fe852595a9e3
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_DISCONNECT_FROM_NETWORK) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c1b260fb81ccb0fd5590aa5022988dbf32e38f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580324"
---
# <a name="hsplugindisconnectfromnetwork-function"></a>HS\_プラグイン\_切断\_FROM\_ネットワーク関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_切断\_FROM\_ネットワーク**関数は、デバイスをネットワークから切断すること、プラグインに通知します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_DISCONNECT_FROM_NETWORK)(
  _In_ HS_NETWORK_IDENTITY *pNetworkIdentity
);
```

<a name="parameters"></a>パラメーター
----------

*\*pNetworkIdentity* \[in\]  
ポインター、 [ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)デバイスを切断する元となるネットワークの構造体。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="requirements"></a>必要条件
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

 

 




