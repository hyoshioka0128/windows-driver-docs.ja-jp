---
title: eHS_AUTHENTICATION_RESULT 列挙型
description: EHS_AUTHENTICATION_RESULT 列挙体は、PostConnectAuth 要求の後、プラグインによって認証の結果を示します。
ms.assetid: a61ddc7c-8df8-410c-83df-9058e88bce51
keywords:
- Windows Vista 以降のドライバーをネットワーク eHS_AUTHENTICATION_RESULT 列挙型
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: e68b8ee341f7cdf903d16eccbff85d44baafe4d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372569"
---
# <a name="ehsauthenticationresult-enumeration"></a>eHS\_認証\_結果の列挙型

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**EHS\_認証\_結果**列挙体の PostConnectAuth 要求の後、プラグインによって認証の結果を示します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef enum _eHS_AUTHENTICATION_RESULT { 
  HS_AUTHENTICATION_RESULT_SUCCESS         = 0,
  HS_AUTHENTICATION_RESULT_FAILED_TIMEOUT  = 100,
  HS_AUTHENTICATION_RESULT_FAILED_AUTH,
  HS_AUTHENTICATION_RESULT_FAILED_CONNECT,
  HS_AUTHENTICATION_RESULT_FAILED_OTHER,
  HS_AUTHENTICATION_RESULT_MAX
} eHS_AUTHENTICATION_RESULT;
```

<a name="constants"></a>定数
---------

<a href="" id="hs-authentication-result-success"></a>**HS\_認証\_結果\_成功**  
認証が成功したことを示します。

<a href="" id="hs-authentication-result-failed-timeout"></a>**HS\_認証\_結果\_FAILED\_タイムアウト**  
サーバー/バックエンドからのタイムアウトにより、認証が失敗したことを示します。

<a href="" id="hs-authentication-result-failed-auth"></a>**HS\_認証\_結果\_FAILED\_認証**  
資格情報が正しくないため、認証が失敗したことを示します。

<a href="" id="hs-authentication-result-failed-connect"></a>**HS\_認証\_結果\_FAILED\_接続**  
認証サーバーに接続することができないのため、認証が失敗したことを示します。

<a href="" id="hs-authentication-result-failed-other"></a>**HS\_認証\_結果\_FAILED\_OTHER**  
何らかの理由で失敗しました。 認証を示します。

<a href="" id="hs-authentication-result-max"></a>**HS\_認証\_結果\_MAX**  
範囲外の値を示します。

<a name="remarks"></a>注釈
-------

プラグインが使用してホット スポットのプラグインのホストにこの列挙値を渡す、 [ **HS\_ホスト\_POST\_CONNECT\_AUTH\_完了**](hs-host-post-connect-auth-completion.md) 、関数の呼び出しの結果のホット スポットのプラグインのホストに通知するために使用[ **HS\_プラグイン\_開始\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md)します。

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
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

 

 




