---
title: Wi-Fi ホット スポット オフロード関数
description: Wi-Fi ホット スポット オフロード関数
ms.assetid: 114e1604-0d9a-418c-aee1-a9b615d13d21
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7aed1acdaae9c12ad6e7f7138df44f8b30dbcdf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385920"
---
# <a name="wi-fi-hotspot-offloading-functions"></a>Wi-Fi ホット スポット オフロード関数

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


このセクションでは、フレームワークの Wi-fi ホット スポットのオフロード機能について説明します。 これらの関数は、プラグインのホット スポットとホット スポットのプラグインのホスト間の対話を容易になります。

次の関数は、プラグインの DLL によってエクスポートされます。

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
<td><p><a href="hsplugingetversion.md" data-raw-source="[HSPluginGetVersion](hsplugingetversion.md)">HSPluginGetVersion</a></p></td>
<td><p>この関数は、プラグインとホストのバージョンが一致するかを確認します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hsplugininitplugin.md" data-raw-source="[HSPluginInitPlugin](hsplugininitplugin.md)">HSPluginInitPlugin</a></p></td>
<td><p>この関数は、プラグインを初期化するためにホストによって呼び出されます。</p></td>
</tr>
</tbody>
</table>

 

プラグインのホット スポットでは、次の関数を公開する、[ホット スポット\_プラグイン\_API](hotspot-plugin-apis.md)構造体。 この構造体は、初期化中に、ホット スポットのプラグインのホストに渡されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><a href="hs-plugin-check-for-updates.md" data-raw-source="[HS_PLUGIN_CHECK_FOR_UPDATES](hs-plugin-check-for-updates.md)">HS_PLUGIN_CHECK_FOR_UPDATES</a></p></td>
<td><p>この関数は、構成の更新をチェックします。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-deinit.md" data-raw-source="[HS_PLUGIN_DEINIT](hs-plugin-deinit.md)">HS_PLUGIN_DEINIT</a></p></td>
<td><p>この関数は通知プラグインすることはアンロードされます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-disconnect-from-network.md" data-raw-source="[HS_PLUGIN_DISCONNECT_FROM_NETWORK](hs-plugin-disconnect-from-network.md)">HS_PLUGIN_DISCONNECT_FROM_NETWORK</a></p></td>
<td><p>この関数は、デバイスはネットワークから切断するときに通知するプラグイン。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-is-hotspot-network.md" data-raw-source="[HS_PLUGIN_IS_HOTSPOT_NETWORK](hs-plugin-is-hotspot-network.md)">HS_PLUGIN_IS_HOTSPOT_NETWORK</a></p></td>
<td><p>この関数は指定されたネットワークがホット スポット ネットワークかどうかを決定ホストによって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-pre-connect-init.md" data-raw-source="[HS_PLUGIN_PRE_CONNECT_INIT](hs-plugin-pre-connect-init.md)">HS_PLUGIN_PRE_CONNECT_INIT</a></p></td>
<td><p>この関数はホット スポット ネットワークへの接続が進行中の場合、その状態を初期化するためにプラグインを通知します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-query-cellular-exception-hosts.md" data-raw-source="[HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS](hs-plugin-query-cellular-exception-hosts.md)">HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS</a></p></td>
<td><p>この関数は、プラグインが必要になります、認証プロセスの一環として移動体通信で接続するホストの一覧を取得します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-query-hidden-network.md" data-raw-source="[HS_PLUGIN_QUERY_HIDDEN_NETWORK](hs-plugin-query-hidden-network.md)">HS_PLUGIN_QUERY_HIDDEN_NETWORK</a></p></td>
<td><p>この関数は、ネットワーク id と非表示のネットワークのネットワーク プロファイルを返します</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-reset.md" data-raw-source="[HS_PLUGIN_RESET](hs-plugin-reset.md)">HS_PLUGIN_RESET</a></p></td>
<td><p>この関数は、プラグインをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-send-keep-alive.md" data-raw-source="[HS_PLUGIN_SEND_KEEP_ALIVE](hs-plugin-send-keep-alive.md)">HS_PLUGIN_SEND_KEEP_ALIVE</a></p></td>
<td><p>この関数は、ネットワーク接続のキープ アライブ メッセージを送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-plugin-start-post-connect-auth.md" data-raw-source="[HS_PLUGIN_START_POST_CONNECT_AUTH](hs-plugin-start-post-connect-auth.md)">HS_PLUGIN_START_POST_CONNECT_AUTH</a></p></td>
<td><p>この関数を実行するいずれかの接続後、ネットワーク経由でデバイスを認証するために必要な認証。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-plugin-stop-post-connect-auth.md" data-raw-source="[HS_PLUGIN_STOP_POST_CONNECT_AUTH](hs-plugin-stop-post-connect-auth.md)">HS_PLUGIN_STOP_POST_CONNECT_AUTH</a></p></td>
<td><p>この関数は、認証プロセスを停止します。</p></td>
</tr>
</tbody>
</table>

 

ホット スポットのプラグインのホストで次の関数を公開する、[ホット スポット\_ホスト\_ハンドラー](hotspot-host-handlers.md)構造体。 この構造体は、ホット スポット プラグインの初期化中にします。

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
<td><p><a href="hs-host-allocate-memory.md" data-raw-source="[HS_HOST_ALLOCATE_MEMORY](hs-host-allocate-memory.md)">HS_HOST_ALLOCATE_MEMORY</a></p></td>
<td><p>この関数は、呼び出し元によって指定されたメモリの量を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-host-free-memory.md" data-raw-source="[HS_HOST_FREE_MEMORY](hs-host-free-memory.md)">HS_HOST_FREE_MEMORY</a></p></td>
<td><p>この関数は、呼び出し元によって割り当てられたメモリを解放します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-host-post-connect-auth-completion.md" data-raw-source="[HS_HOST_POST_CONNECT_AUTH_COMPLETION](hs-host-post-connect-auth-completion.md)">HS_HOST_POST_CONNECT_AUTH_COMPLETION</a></p></td>
<td><p>この関数は、認証の試行の成否を示します。</p></td>
</tr>
<tr class="even">
<td><p><a href="hs-host-send-keep-alive-completion.md" data-raw-source="[HS_HOST_SEND_KEEP_ALIVE_COMPLETION](hs-host-send-keep-alive-completion.md)">HS_HOST_SEND_KEEP_ALIVE_COMPLETION</a></p></td>
<td><p>この関数は、「送信キープ アライブ」要求の成否を示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hs-host-update-configuration-completion.md" data-raw-source="[HS_HOST_UPDATE_CONFIGURATION_COMPLETION](hs-host-update-configuration-completion.md)">HS_HOST_UPDATE_CONFIGURATION_COMPLETION</a></p></td>
<td><p>この関数は、「更新プログラムの確認」要求の成否を示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Wi-fi ホット スポットの参照をオフロードします。](wi-fi-hotspot-offloading-reference.md)  



