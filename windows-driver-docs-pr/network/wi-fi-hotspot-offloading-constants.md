---
title: Wi-Fi ホット スポット オフロード定数
description: このセクションでは、Wi-fi ホット スポットのオフロード フレームワークに対して定義されている定数について説明します。
ms.assetid: F09DCB81-C9FF-493B-AE8F-97DE441A4BC3
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: c692c307188c4574bc592470b5cb36331ac8877a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365698"
---
# <a name="wi-fi-hotspot-offloading-constants"></a>Wi-Fi ホット スポット オフロード定数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

このセクションでは、Wi-fi ホット スポットのオフロード フレームワークに対して定義されている定数について説明します。

<a href="" id="hs-const-host-current-api-version"></a>**HS\_CONST\_ホスト\_現在\_API\_バージョン**  
1  
現在の API バージョン番号。

<a href="" id="hs-const-max-network-display-name-length"></a>**HS\_CONST\_最大\_ネットワーク\_表示\_名前\_長さ**  
32  
ネットワークの表示名の文字列の最大長。

<a href="" id="hs-const-max-realm-length"></a>**HS\_CONST\_最大\_レルム\_長さ**  
255  
領域の値の文字列の最大長。

<a href="" id="hs-const-min-conn-keepalive-time-in-mins"></a>**HS\_CONST\_MIN\_CONN\_KEEPALIVE\_時間\_IN\_(分)**  
5  
キープ アライブ メッセージの転送間隔の最短時間

<a href="" id="hs-const-profile-update-time-in-days"></a>**HS\_CONST\_プロファイル\_UPDATE\_時間\_IN\_日**  
7  
プロファイルの更新プログラムのチェック間隔の最短時間。

<a href="" id="hs-const-min-network-priority-value"></a>**HS\_CONST\_MIN\_ネットワーク\_優先度\_値**  
1  
ネットワークの最小優先度の値。

<a href="" id="hs-const-max-network-priority-value"></a>**HS\_CONST\_最大\_ネットワーク\_優先度\_値**  
65000  
最大ネットワークの優先度の値。

<a href="" id="hs-max-phone-number-length"></a>**HS\_最大\_PHONE\_数\_長さ**  
32  
電話番号の文字列の最大長。

<a href="" id="hs-const-max-host-name-length"></a>**HS\_CONST\_最大\_ホスト\_名前\_長さ**  
255  
ホスト名の文字列の最大長。

<a href="" id="hs-const-plugin-min-rank-value"></a>**HS\_CONST\_プラグイン\_MIN\_ランク\_値**  
1  
順位付けの最小値。 0 より大きくなければなりません。

<a href="" id="hs-const-plugin-max-rank-value"></a>**HS\_CONST\_プラグイン\_最大\_ランク\_値**  
250  
順位付けの最大値。 250 以下である必要があります。

<a href="" id="hs-const-max-provider-name-length"></a>**HS\_CONST\_最大\_プロバイダー\_名前\_長さ**  
63  
プロバイダー名文字列の最大長。

<a href="" id="hs-const-max-advanced-page-string-length"></a>**HS\_CONST\_最大\_詳細\_ページ\_文字列\_長さ**  
255  
詳細設定 ページの文字列の最大長。

<a href="" id="hs-const-max-phone-number-length"></a>**HS\_CONST\_最大\_PHONE\_数\_長さ**  
32  
電話番号の文字列の最大長。

<a href="" id="hs-const-max-supported-sims"></a>**HS\_CONST\_最大\_サポートされている\_SIM**  
1000  
SIM でサポートされる構成の一覧の最大サイズ。

<a href="" id="hs-const-max-cellular-exception-hosts"></a>**HS\_CONST\_最大\_移動体通信\_例外\_ホスト**  
5  
移動体通信担ぎの一覧の最大サイズ。

<a href="" id="hs-const-max-auth-error-msg-length"></a>**HS\_CONST\_最大\_AUTH\_エラー\_MSG\_長さ**  
512  
認証エラー メッセージの最大長。

<a href="" id="hs-const-max-user-messages-in-minutes"></a>**HS\_CONST\_最大\_ユーザー\_メッセージ\_IN\_分**  
7\*24\*60  
分 (7 日間) で、最大のユーザーのメッセージ

次のフラグは、プラグインとそれらの要件と機能をそれぞれ示すホストに対して定義されます。

<a href="" id="hs-flag-capability-network-type-visible"></a>**HS\_フラグ\_機能\_ネットワーク\_型\_VISIBLE**  
0x00000001  
表示されるネットワークを指定します。

<a href="" id="hs-flag-capability-network-type-hidden"></a>**HS\_フラグ\_機能\_ネットワーク\_型\_非表示**  
0x00000002  
非表示のネットワークを指定します。

<a href="" id="hs-flag-capability-network-display-name"></a>**HS\_フラグ\_機能\_ネットワーク\_表示\_名**  
0x00000010  
EAP SIM または EAP AKA 認証の表示名の使用を指定します。

<a href="" id="hs-flag-capability-network-auth-no-sim"></a>**HS\_フラグ\_機能\_ネットワーク\_AUTH\_いいえ\_SIM**  
0x00000100  
いいえ、SIM 認証を指定します。

<a href="" id="hs-flag-capability-network-auth-http"></a>**HS\_フラグ\_機能\_ネットワーク\_AUTH\_HTTP**  
0x00000200  
HTTP 認証を指定します。

<a href="" id="hs-flag-capability-network-auth-eap-sim"></a>**HS\_フラグ\_機能\_ネットワーク\_AUTH\_EAP\_SIM**  
0x00001000  
EAP SIM 認証を指定します。

<a href="" id="hs-flag-capability-network-auth-eap-aka"></a>**HS\_フラグ\_機能\_ネットワーク\_AUTH\_EAP\_別名**  
0x00002000  
EAP-AKA の認証を指定します。

<a href="" id="hs-flag-capability-network-auth-eap-aka-prime"></a>**HS\_フラグ\_機能\_ネットワーク\_AUTH\_EAP\_AKA\_素数**  
0x00004000  
指定 EAP AKA' (AKA Prime) 認証します。

<a href="" id="hs-flag-capability-network-custom-realm"></a>**HS\_フラグ\_機能\_ネットワーク\_カスタム\_領域**  
0x00010000  
ネットワーク認証のためのカスタムの領域の値の使用を指定します。

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
<td><p>Windows 10 Mobile</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[Wi-fi ホット スポットの参照をオフロードします。](wi-fi-hotspot-offloading-reference.md)

 

 




