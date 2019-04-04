---
title: HS_NETWORK_PROFILE 構造体
description: HS_NETWORK_PROFILE 構造では、プラグインによって提供され、ターゲット ネットワークに接続するために必要な情報が含まれています。 ネットワーク プロファイルの各インスタンスは、対応する HS_NETWORK_IDENTITY 構造に一意に関連付けられます。
ms.assetid: 55e8786c-d7b8-48f3-9e54-312183cf8fb3
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_NETWORK_PROFILE 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_NETWORK_PROFILE 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef670ed92132114119174230fc78532fe5ca6e44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578731"
---
# <a name="hsnetworkprofile-structure"></a>HS\_ネットワーク\_プロファイルの構造

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_ネットワーク\_プロファイル**構造は、プラグインによって提供され、ターゲット ネットワークに接続するために必要な情報が含まれています。 ネットワーク プロファイルの各インスタンスは一意に対応する関連付けられている[ **HS\_ネットワーク\_IDENTITY** ](hs-network-identity.md)構造体。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_NETWORK_PROFILE {
  DWORD  dwNetworkCapabilities;
  USHORT usPriority;
  DWORD  dwSupportedSIMCount;
  DWORD  dmNumCellularExceptions;
  DWORD  dwNetworkStringID;
  DWORD  dwKeepAliveTimeMins;
  WCHAR  szRealm[HS_CONST_MAX_REALM_LENGTH+1];
} HS_NETWORK_PROFILE, *PHS_NETWORK_PROFILE;
```

<a name="members"></a>メンバー
-------

**dwNetworkCapabilities**  
使用可能なサブセット**HS\_フラグ\_機能\_ネットワーク\_\\*** 値。 ホット スポットのホスト機能の詳細については、[ **Wi-fi ホット スポットのオフロード定数**](wi-fi-hotspot-offloading-constants.md)を参照してください。

**usPriority**  
関連付けられているネットワークに割り当てられている固有の優先順位の値。 1 ~ 65000 (非表示のネットワークは、値 1 が必要) の値があります。 小さい数値は高い優先順位に対応します。

**dwSupportedSIMCount**  
サポートされている SIM 数。 このメンバーは、HTTP ベースおよび EAP SIM/別名または別名の設定が ' 認証します。

**dmNumCellularExceptions**  
任意。 移動体通信のみでホスト接続の数。

**dwNetworkStringID**  
ネットワーク名の文字列 id です。 文字列の最大サイズ = 最大\_ネットワーク\_表示\_名前\_長さ。

**dwKeepAliveTimeMins**  
任意。 ネットワーク接続のキープ アライブ メッセージの時間間隔。

**szRealm**  
ネットワーク固有の領域の値。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**HS\_ネットワーク\_IDENTITY**](hs-network-identity.md)

[**Wi-fi ホット スポットの定数がオフロード**](wi-fi-hotspot-offloading-constants.md)

 

 




