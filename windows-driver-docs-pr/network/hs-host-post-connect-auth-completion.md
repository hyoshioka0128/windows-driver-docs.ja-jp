---
title: HS_HOST_POST_CONNECT_AUTH_COMPLETION 関数
description: HS_HOST_POST_CONNECT_AUTH_COMPLETION 関数は、次の Wi-fi 接続のセットアップを層 2 では、認証試行の成否を示します。
ms.assetid: 2c69802b-968b-400c-b02c-c2d39fa51d5a
keywords:
- Windows Vista 以降のドライバーをネットワーク typedef DWORD (WINAPI HS_HOST_POST_CONNECT_AUTH_COMPLETION) 関数
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e538fc9bbec138e7f7de0fae9117c2b1b00e5c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558866"
---
# <a name="hshostpostconnectauthcompletion-function"></a>HS\_ホスト\_POST\_CONNECT\_AUTH\_完了関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ホスト\_POST\_CONNECT\_AUTH\_完了**関数は、次の Wi-fi 接続、認証試行の成否を示します。レイヤー 2 でセットアップします。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
 typedef DWORD (WINAPI *HS_HOST_POST_CONNECT_AUTH_COMPLETION)(
  _In_     HANDLE                    hPluginContext,
  _In_     DWORD                     dwConnectionId,
  _In_     eHS_AUTHENTICATION_RESULT AuthResult,
  _In_opt_ LPVOID                    pvReserved
);
```

<a name="parameters"></a>パラメーター
----------

*hPluginContext* \[in\]  
この関数を呼び出すプラグインのコンテキスト ハンドル。

*dwConnectionId* \[in\]  
ネットワーク接続の一意の識別子。

*AuthResult* \[で\]  
[ **EHS\_認証\_結果**](ehs-authentication-result.md)成功または失敗を示す列挙値。

*pvReserved* \[で、省略可能\]  
将来使用するために予約されています。

<a name="return-value"></a>戻り値
------------

この関数は、ホストと通信するようにプラグインによって呼び出され、値は返されません。

<a name="remarks"></a>注釈
-------

このプラグインは、以前の呼び出しの結果のホストに通知するには、この関数を呼び出す必要があります[ **HS\_プラグイン\_開始\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md).

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


[**eHS\_認証\_結果**](ehs-authentication-result.md)

[**HS\_プラグイン\_開始\_POST\_CONNECT\_認証**](hs-plugin-start-post-connect-auth.md)

 

 




