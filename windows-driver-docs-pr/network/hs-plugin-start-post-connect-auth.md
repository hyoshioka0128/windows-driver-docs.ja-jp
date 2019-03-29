---
title: HS_PLUGIN_START_POST_CONNECT_AUTH 関数
description: HS_PLUGIN_START_POST_CONNECT_AUTH 関数の呼び出しを実行するいずれかの接続後、ネットワーク経由でデバイスを認証するために必要な認証。
ms.assetid: f52236fc-2afd-46e2-ae88-7c4fa10f8d59
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_PLUGIN_START_POST_CONNECT_AUTH) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeeecb7294e73222600df3762addb7b36ed55ce8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574337"
---
# <a name="hspluginstartpostconnectauth-function"></a>HS\_プラグイン\_開始\_POST\_CONNECT\_AUTH 関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_プラグイン\_開始\_POST\_CONNECT\_AUTH**関数を呼び出すを実行するいずれかの接続後の接続経由でデバイスを認証するために必要な認証ネットワーク。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_PLUGIN_START_POST_CONNECT_AUTH)(
  _In_ DWORD                 dwConnectionId,
  _In_ HS_CONNECTION_CONTEXT *pConnectContext,
  _In_ HS_SIM_DATA           *pSIMData,
  _In_ HS_NETWORK_IDENTITY   *pNetworkIdentity,
  _In_ HS_NETWORK_PROFILE    *pNetworkProfile
);
```

<a name="parameters"></a>パラメーター
----------

*dwConnectionId* \[in\]  
ネットワーク接続の一意の識別子。

*\*pConnectContext* \[in\]  
ポインターを[ **HS\_接続\_コンテキスト**](hs-connection-context.md)接続の認証後に実行用のプラグインで必要な情報を含む構造体。

*\*pSIMData* \[in\]  
ポインターを[ **HS\_SIM\_データ**](hs-sim-data.md)接続の認証後に実行用のプラグインで必要な SIM から情報を含む構造体。

*\*pNetworkIdentity* \[in\]  
ポインター、 [ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)ネットワークの構造体。

*\*pNetworkProfile* \[in\]  
ポインター、 [ **HS\_ネットワーク\_プロファイル**](hs-network-profile.md)ネットワーク プロファイルを含む構造体。

<a name="return-value"></a>戻り値
------------

この関数は、プラグインを使用して通信するためにホストによって呼び出され、値は返されません。

<a name="remarks"></a>コメント
-------

この関数を呼び出した後、プラグインを呼び出す必要があります、 [ **HS\_ホスト\_POST\_CONNECT\_AUTH\_完了**](hs-host-post-connect-auth-completion.md)ハンドラー要求の状態のホストに通知します。

ネットワークでは、EAP-SIM/AKA 認証を使用する場合、プラグインでは、この状態で任意のアクティビティを実行する必要はありません。 ただし、ネットワークには、HTTP ベースの認証が必要とする場合、プラグインは、適切な認証を実行する必要があります。

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


[**HS\_接続\_コンテキスト**](hs-connection-context.md)

[**HS\_SIM\_データ**](hs-sim-data.md)

[**HS\_ネットワーク\_IDENTITY**](hs-network-identity.md)

[**HS\_ネットワーク\_プロファイル**](hs-network-profile.md)

 

 




