---
title: HS_PLUGIN_QUERY_HIDDEN_NETWORK 関数
description: HS_PLUGIN_QUERY_HIDDEN_NETWORK 関数は、ネットワーク id と非表示のネットワークのネットワーク プロファイルを返します。
ms.assetid: edf5ddb0-22f6-4c24-a118-3915a1f2b0af
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_QUERY_HIDDEN_NETWORK) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bcfcfef1f2fd519a2123bb8654a616744729563
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571974"
---
# <a name="hspluginqueryhiddennetwork-function"></a>HS\_プラグイン\_クエリ\_HIDDEN\_ネットワーク関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_クエリ\_HIDDEN\_ネットワーク**関数は、ネットワーク id と非表示のネットワークのネットワーク プロファイルを返します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_QUERY_HIDDEN_NETWORK)(
  _Out_ HS_NETWORK_IDENTITY *pHiddenNetworkIdentity,
  _Out_ HS_NETWORK_PROFILE  *pHiddenNetworkProfile
);
```

<a name="parameters"></a>パラメーター
----------

*\*pHiddenNetworkIdentity* \[out\]  
[ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)ネットワークを一意に識別する構造体。

*\*pHiddenNetworkProfile* \[out\]  
[ **HS\_ネットワーク\_プロファイル**](hs-network-profile.md)ネットワーク プロファイルを含む構造体。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="remarks"></a>コメント
-------

ホストが場合にのみ、この関数を呼び出して、 **dwPluginCapabilities**フィールドの関連付けられているプラグインの[ **HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体が含まれています、 **HS\_フラグ\_機能\_ネットワーク\_型\_HIDDEN**機能します。

プラグインでは、非表示の Wi-fi ネットワークのネットワーク id と、ネットワーク プロファイルの両方を提供する必要があります。

このネットワークには、すべてのホット スポット ネットワーク間で最高の優先順位 (1) 必要があります。

ホット スポットのオフロード サービスで、サービスのライフ サイクルの 1 つの非表示のネットワークの制限が課せられます。 そのため、大文字と小文字の非表示のネットワークを指定する最初のプラグインの要求のみが受け入れられる、複数のプラグインがインストールされている場合は。

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

[**HS\_ネットワーク\_プロファイル**](hs-network-profile.md)

[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

 

 




