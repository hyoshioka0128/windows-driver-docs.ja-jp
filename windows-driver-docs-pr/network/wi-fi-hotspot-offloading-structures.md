---
title: Wi-Fi ホット スポット オフロード構造
description: Wi-Fi ホット スポット オフロード構造
ms.assetid: 7ec80296-1ac9-48df-a250-6fd856c57901
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fe098d8f5a42877a01068d91b4fc5d7c39940b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378726"
---
# <a name="wi-fi-hotspot-offloading-structures"></a>Wi-Fi ホット スポット オフロード構造

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

このセクションでは、Wi-fi ホット スポットのオフロード framework のデータ構造について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hotspot-host-handlers.md" data-raw-source="[HOTSPOT_HOST_HANDLERS](hotspot-host-handlers.md)">HOTSPOT_HOST_HANDLERS</a></p></td>
<td><p>この構造体には、ホット スポット ホスト ハンドラー関数のテーブルが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hotspot-plugin-apis.md" data-raw-source="[HOTSPOT_PLUGIN_APIS](hotspot-plugin-apis.md)">HOTSPOT_PLUGIN_APIS</a></p></td>
<td><p>この構造体には、ホット スポットのプラグイン Api 関数テーブルが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-connection-context.md" data-raw-source="[HS_CONNECTION_CONTEXT](hs-connection-context.md)">HS_CONNECTION_CONTEXT</a></p></td>
<td><p>この構造体には、プラグインによって post connect 認証するために必要な情報が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-device-identity.md" data-raw-source="[HS_DEVICE_IDENTITY](hs-device-identity.md)">HS_DEVICE_IDENTITY</a></p></td>
<td><p>この構造体には、デバイスの製造元、電話のモデルについての情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-mac-address.md" data-raw-source="[HS_MAC_ADDRESS](hs-mac-address.md)">HS_MAC_ADDRESS</a></p></td>
<td><p>この構造体には、ホスト メディア アクセス コントロール (MAC) アドレスにはが含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-network-identity.md" data-raw-source="[HS_NETWORK_IDENTITY](hs-network-identity.md)">HS_NETWORK_IDENTITY</a></p></td>
<td><p>この構造体には、Wi-fi ネットワークを一意に識別する情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-network-profile.md" data-raw-source="[HS_NETWORK_PROFILE](hs-network-profile.md)">HS_NETWORK_PROFILE</a></p></td>
<td><p>この構造体には、接続に必要な情報が含まれています。 ターゲット ネットワーク。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-cellular-exception-hosts.md" data-raw-source="[HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS](hs-plugin-cellular-exception-hosts.md)">HS_PLUGIN_CELLULAR_EXCEPTION_HOSTS</a></p></td>
<td><p>この構造体には、プラグインする必要がありますが接続する携帯電話のベアラー経由でホストの一覧が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-host-name.md" data-raw-source="[HS_PLUGIN_HOST_NAME](hs-plugin-host-name.md)">HS_PLUGIN_HOST_NAME</a></p></td>
<td><p>この構造体には、ホスト名が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-profile.md" data-raw-source="[HS_PLUGIN_PROFILE](hs-plugin-profile.md)">HS_PLUGIN_PROFILE</a></p></td>
<td><p>この構造体には、プラグインについての情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-supported-sims.md" data-raw-source="[HS_PLUGIN_SUPPORTED_SIMS](hs-plugin-supported-sims.md)">HS_PLUGIN_SUPPORTED_SIMS</a></p></td>
<td><p>この構造体には、SIM でサポートされる構成の一覧が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-version.md" data-raw-source="[HS_PLUGIN_VERSION](hs-plugin-version.md)">HS_PLUGIN_VERSION</a></p></td>
<td><p>この構造体には、プラグインでサポートされる最小値と最大のホット スポットのホストのバージョンが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-sim-data.md" data-raw-source="[HS_SIM_DATA](hs-sim-data.md)">HS_SIM_DATA</a></p></td>
<td><p>この構造体には、SIM カードから取得した id 情報が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-sim-identity.md" data-raw-source="[HS_SIM_IDENTITY](hs-sim-identity.md)">HS_SIM_IDENTITY</a></p></td>
<td><p>この構造体には、EAP SIM または EAP-AKA の認証に必要な SIM 識別情報が含まれています。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Wi-fi ホット スポットの参照をオフロードします。](wi-fi-hotspot-offloading-reference.md)  



