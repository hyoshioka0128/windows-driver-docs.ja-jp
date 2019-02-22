---
title: HOTSPOT_PLUGIN_APIS 構造体
description: HOTSPOT_PLUGIN_APIS 構造体には、ホット スポット プラグイン Api 関数のテーブルが含まれています。
ms.assetid: eee56f84-2c7f-4218-b7ec-b4fc0181d767
keywords:
- Windows Vista 以降のドライバーをネットワーク HOTSPOT_PLUGIN_APIS が構造体します。
- Windows Vista 以降のドライバーをネットワーク PHOTSPOT_PLUGIN_APIS 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fdf2e93ad7904b221b5eb714fb92230329caa28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560827"
---
# <a name="hotspotpluginapis-structure"></a>ホット スポット\_プラグイン\_API 構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**ホット スポット\_プラグイン\_API**構造体には、ホット スポットのプラグイン Api 関数テーブルが含まれています。 この関数のテーブルは、プラグインによって返されるときに[ **HSPluginInitPlugin** ](hsplugininitplugin.md)プラグインを初期化します。 テーブルには、プラグインを使用して通信するために、ホット スポット ホストによって呼び出される関数が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HOTSPOT_PLUGIN_APIS {
  HS_PLUGIN_QUERY_SUPPORTED_SIMS     HSPluginQuerySupportedSIMs;
  HS_PLUGIN_QUERY_HIDDEN_NETWORK     HSPluginQueryCellularExceptionHosts;
  HS_PLUGIN_IS_HOTSPOT_NETWORK       HSPluginIsHotspotNetwork;
  HS_PLUGIN_PRE_CONNECT_INIT         HSPluginPreConnectInit;
  HS_PLUGIN_START_POST_CONNECT_AUTH  HSPluginStartPostConnectAuth;
  HS_PLUGIN_STOP_POST_CONNECT_AUTH   HSPluginStopPostConnectAuth;
  HS_PLUGIN_DISCONNECT_FROM_NETWORK  HSPluginDisconnectFromNetwork;
  HS_PLUGIN_RESET                    HSPluginReset;
  HS_PLUGIN_SEND_KEEP_ALIVE          HSPluginSendKeepAlive;
  HS_PLUGIN_CHECK_FOR_UPDATES        HSPluginCheckForUpdates;
  HS_PLUGIN_DEINIT                   HSPluginDeinit;
} HOTSPOT_PLUGIN_APIS, *PHOTSPOT_PLUGIN_APIS;
```

<a name="members"></a>Members
-------

**HSPluginQuerySupportedSIMs**  
API は、プラグインの初期化中に呼び出されます。

プラグインをサポートする Sim の一覧を取得する、ホット スポット ホストによって呼び出されます。 Sim のサポートされている、または特定のネットワークの Sim だけの完全な一覧を取得することと呼ばれることができます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_クエリ\_サポートされている\_SIM**](hs-plugin-query-supported-sims.md)します。

**HSPluginQueryCellularExceptionHosts**  
API は、プラグインの初期化中に呼び出されます。

プラグインが指定されている場合に、ホット スポット ホストによって呼び出されます、 **HS\_フラグ\_機能\_ネットワーク\_型\_HIDDEN**での機能、 [**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)構造体。 詳細については、次を参照してください。 [ **HS\_プラグイン\_クエリ\_HIDDEN\_ネットワーク**](hs-plugin-query-hidden-network.md)します。

**HSPluginIsHotspotNetwork**  
API は、スキャン結果の処理中に呼び出されます。

ネットワークが渡された場合を識別するためにプラグインを要求するホット スポット ホストによって呼び出されます、 *pHiddenNetworkIdentity*パラメーターは、ホット スポット ネットワーク。 詳細については、次を参照してください。 [ **HS\_プラグイン\_IS\_ホット スポット\_ネットワーク**](hs-plugin-is-hotspot-network.md)します。

**HSPluginPreConnectInit**  
接続プロセスの API です。

接続が進行中のときの状態を初期化するためにプラグインを通知する、ホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_PRE\_CONNECT\_INIT**](hs-plugin-pre-connect-init.md)します。

**HSPluginStartPostConnectAuth**  
接続プロセスの API です。

呼ばれる要求を実行するようにプラグインするホット スポットのホストがいずれかの接続後、ネットワーク経由でデバイスを認証するために必要な認証。 詳細については、次を参照してください。 [ **HS\_プラグイン\_開始\_POST\_CONNECT\_AUTH**](hs-plugin-start-post-connect-auth.md)します。

**HSPluginStopPostConnectAuth**  
接続プロセスの API です。

認証プロセスを停止するプラグインに通知する、ホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_停止\_POST\_CONNECT\_AUTH**](hs-plugin-stop-post-connect-auth.md)します。

**HSPluginDisconnectFromNetwork**  
接続プロセスの API です。

ネットワークから切断のプラグインに通知する、ホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_切断\_FROM\_ネットワーク**](hs-plugin-disconnect-from-network.md)します。

**HSPluginReset**  
プラグインをリセットする API です。 プラグインがこの呼び出しから戻る前に保留中の呼び出しを解放しない場合、プラグインはアンロードされます。

プラグインをリセットするホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_リセット**](hs-plugin-reset.md)します。

**HSPluginSendKeepAlive**  
定期的な更新プログラムを実行するプラグインの API です。

プラグインをキープ アライブ メッセージを送信する、ホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_送信\_保持\_ALIVE**](hs-plugin-send-keep-alive.md)します。

**HSPluginCheckForUpdates**  
定期的な更新プログラムを実行するプラグインの API です。

更新プログラムを確認する、ホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_確認\_の\_更新**](hs-plugin-check-for-updates.md)します。

**HSPluginDeinit**  
初期化を解除し、アンロードの前に、プラグインをクリーンアップする API が呼び出されます。

アンロードしようとしていますが、プラグインを通知する、ホット スポット ホストによって呼び出されます。 詳細については、次を参照してください。 [ **HS\_プラグイン\_DEINIT**](hs-plugin-deinit.md)します。

<a name="requirements"></a>要件
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


[**HSPluginInitPlugin**](hsplugininitplugin.md)

[**HS\_プラグイン\_クエリ\_サポートされている\_SIM**](hs-plugin-query-supported-sims.md)

[**HS\_プラグイン\_プロファイル**](hs-plugin-profile.md)

[**HS\_プラグイン\_クエリ\_HIDDEN\_ネットワーク**](hs-plugin-query-hidden-network.md)

[**HS\_プラグイン\_IS\_ホット スポット\_ネットワーク**](hs-plugin-is-hotspot-network.md)

[**HS\_プラグイン\_PRE\_CONNECT\_INIT**](hs-plugin-pre-connect-init.md)

[**HS\_プラグイン\_開始\_POST\_CONNECT\_認証**](hs-plugin-start-post-connect-auth.md)

[**HS\_プラグイン\_停止\_POST\_CONNECT\_認証**](hs-plugin-stop-post-connect-auth.md)

[**HS\_プラグイン\_切断\_FROM\_ネットワーク**](hs-plugin-disconnect-from-network.md)

[**HS\_プラグイン\_リセット**](hs-plugin-reset.md)

[**HS\_プラグイン\_送信\_保持\_ALIVE**](hs-plugin-send-keep-alive.md)

[**HS\_プラグイン\_確認\_の\_更新プログラム**](hs-plugin-check-for-updates.md)

[**HS\_プラグイン\_DEINIT**](hs-plugin-deinit.md)

 

 




