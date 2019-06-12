---
title: Wi-Fi ホット スポット オフロード プラグイン
description: Wi-Fi ホット スポット オフロード プラグイン
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 819f145063563487cdbef6fcd212c0761aa59ad7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379164"
---
# <a name="wi-fi-hotspot-offloading-plugin"></a>Wi-Fi ホット スポット オフロード プラグイン

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]

Wi-fi のオフロードを有効にするには、作成し、ホット スポットのプラグインをインストールします。 このトピックでは、ホット スポットのプラグインを開発する際に考慮すべき問題のいくつかについて説明します。 プラグインのプラグイン パッケージの一部として実装される Api の一般的な説明も提供します。

## <a name="planning-the-plugin"></a>プラグインの計画

プラグインの開発を開始する前に、次の問題に対処することを確認します。

### <a name="supported-authentication-methods"></a>サポートされている認証方法

プラグインをサポートするネットワークで必要な認証方法を特定します。 ホット スポットのオフロード フレームワークには、ネットワークの 3 つのクラスがサポートされています。

* WISPr 1.0、またはいくつかのバリエーションでは、HTTP 経由でのユーザーまたはデバイスの認証を使用してネットワーク。 これらのネットワークは、次の機能によって表されます。
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_HTTP**
* EAP SIM/別名または別名を使用したネットワーク ' デバイスを認証します。 これらのネットワークは、次の機能によって表されます。
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_SIM**
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_AKA**
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_EAP_AKA_PRIME**

  EAP ベースのネットワークでは、プラグインも指定できます、カスタムの領域を使用して、 **HS_FLAG_CAPABILITY_NETWORK_CUSTOM_REALM**機能します。

* 認証またはネットワーク プラグインが任意のデバイスの資格情報を必要としない独立した認証メカニズムが必要としないネットワーク。 これらのネットワークは、次の機能によって表されます。
  * **HS_FLAG_CAPABILITY_NETWORK_AUTH_NO_SIM**

### <a name="hidden-networks"></a>非表示のネットワーク

ネットワークが、スキャンの結果に表示されないために、初期化時に非表示のネットワークの予め指定をされた必要があります。 非表示のネットワークの電源とプライバシーの実装、により、フレームワークでは最大で 1 つの非表示ネットワークがグローバルにサポートします。 そのため、別のプラグインが非表示のネットワークへの接続を要求しても、2 番目のプラグインの要求が拒否されます。 これを指定する必要があるかどうか、プラグインは非表示のネットワークを構成する必要があります、 **HS_FLAG_CAPABILITY_NETWORK_TYPE_HIDDEN**そのネットワークの機能です。

その他のすべてのネットワークの場合は、プラグインを指定する必要があります、 **HS_FLAG_CAPABILITY_NETWORK_TYPE_VISIBLE**機能します。

### <a name="user-interface-display-strings"></a>ユーザー インターフェイスの表示文字列

プラグインによって、ユーザーとの通信に使用されるカスタムの UI 表示文字列は、(.rc ファイル) 内の文字列テーブルに格納する必要があります。 プラグインは、文字列 Id を適切な文字列の読み込みを有効にする、ホット スポットのオフロード サービスに渡す必要があります。 現時点では、次の表示文字列がサポートされています。

* プロバイダー名 (最大**HS_CONST_MAX_PROVIDER_NAME_LENGTH**長さ)
* ネットワーク名 (最大**HS_CONST_MAX_NETWORK_DISPLAY_NAME_LENGTH**長さ)
* メッセージの詳細 ページ (最大**HS_CONST_MAX_ADVANCED_PAGE_STRING_LENGTH**長さ)
* HSHostSendUserMessage 関数を使用してユーザーに渡された追加の文字列 (最大**最大\_パス**長さ)。 詳細については、次を参照してください。 [HS_HOST_SEND_USER_MESSAGE](https://msdn.microsoft.com/library/windows/hardware/dn789353)します。

**注:** Wi-fi ホット スポットのオフロード機能と定数の詳細については、次を参照してください。 [Wi-fi ホット スポットのオフロード定数](https://msdn.microsoft.com/library/windows/hardware/mt800328)します。

## <a name="implementing-the-plugin"></a>プラグインを実装します。

このプラグインは、DLL として実装されます。 関数は、 [HSPluginGetVersion](https://msdn.microsoft.com/library/windows/hardware/dn789345)と[HSPluginInitPlugin](https://msdn.microsoft.com/library/windows/hardware/dn789346)プラグイン DLL の .def ファイルで指定するかで「方式」を追加することで公開されている必要があります、関数の実装。

## <a name="initialization"></a>初期化

初期化の時点では、次の順序では、プラグインの Api が呼び出されます。

### <a name="hsplugingetversion"></a>HsPluginGetVersion

プラグインは、プラグインのバージョンが、ホスト デバイスのバージョンと一致することを確認するためののバージョン情報を返す必要があります。 現在のバージョンが、定数に格納されている**HS_CONST_HOST_CURRENT_API_VERSION**します。

### <a name="hsplugininitplugin"></a>HSPluginInitPlugin

これはメインの初期化関数です。 プラグインには、次の情報を提供します。

* ホット スポットのプラグインのホストのいずれかが呼び出されるたびに使用するプラグインのコンテキスト ハンドル (* * HS_HOST_\*\\* * *) 関数
* 現在、ホストによって使用されているバージョン番号 (**dwVerNumUsed**)
* デバイスに関する情報 (**pDeviceIdentity**)
* HS_FLAG_CAPABILITY_NETWORK_ * * 型として指定された、プラグインを使用できる OS 機能 (**dwHostCapabilities**)
* ホストにコールバックするプラグインで使用される関数のハンドラー (**pHotspotHostHandlers**)

プラグインには、ホット スポットのプラグインのホストに、次の情報が返されます。

* プラグインの Api の一覧を含む構造体へのポインター (**pHotspotPluginAPIs**)。 詳細については、次を参照してください。 [HOTSPOT_PLUGIN_APIS](https://msdn.microsoft.com/library/windows/hardware/dn789344)します。
* プラグインのプロファイルを格納する構造体へのポインター (**pPluginProfile**)。 詳細については、次を参照してください。 [HS_PLUGIN_PROFILE](https://msdn.microsoft.com/library/windows/hardware/dn789365)します。 

プロファイルには、すべてのプラグインが必要な機能が含まれます。 これは、該当する機能フラグの値を組み合わせることによって生成される 1 つの値によって表されます (HS_FLAG_CAPABILITY_NETWORK_\*)、ビットごとの OR 演算を使用しています。 場合は、プラグインの指定、HS\_フラグ\_機能\_ネットワーク\_AUTH\_HTTP 機能や、HS\_フラグ\_機能\_ネットワーク\_AUTH\_EAP\_ \* 、機能、 **dwSupportedSIMCount**のメンバー、 **HS_PLUGIN_PROFILE**構造体は、数に設定する必要がありますサポートされている Sim。 プラグインは、設定をサポートしているネットワークの合計数も指定する必要があります、 **dwNumNetworksSupported**のメンバー、 **HS_PLUGIN_PROFILE**構造体。

### <a name="hspluginqueryhiddennetwork-optional"></a>HsPluginQueryHiddenNetwork [省略可能]

プラグインを指定する場合、 **HS_FLAG_CAPABILITY_NETWORK_TYPE_HIDDEN**機能と、デバイスが非表示のネットワークをサポートできますが、この関数は、ホット スポット プラグインのホストから非表示のネットワーク情報を取得しますプラグイン。 詳細については、次を参照してください。 [HS_PLUGIN_QUERY_HIDDEN_NETWORK](https://msdn.microsoft.com/library/windows/hardware/dn789367)します。

### <a name="hspluginquerysupportedsims-optional"></a>HsPluginQuerySupportedSIMs [省略可能]

ホット スポットのプラグインのホストが、プラグインが 0 以外の値を指定する場合、この関数を呼び出す**dwSupportedSIMCount**します。 が呼び出されると、 **pNetworkIdentity**引数が NULL にする必要があり、プラグインによってサポートされているすべての Sim の一覧を提供するプラグインが必要です。 この関数が各ホット スポット ネットワークに関連付けられている Sim を識別するために後で呼び出すことも可能性があります (その時点で、 **pNetworkIdentity**非 NULL になります)。 プラグインには、サポートされている Sim の一覧を指定する必要があります。 詳細については、次を参照してください。 [HS_PLUGIN_QUERY_SUPPORTED_SIMS](https://msdn.microsoft.com/library/windows/hardware/dn789368)します。

## <a name="run-time"></a>実行時

ネットワークの表示になると、ホット スポットのプラグインのホストは、ホット スポット ネットワークがかどうかを判断するには、各ネットワーク用のプラグインを照会します。

### <a name="hspluginishotspotnetwork"></a>HSPluginIsHotspotNetwork

ホット スポットのプラグインのホストでは、指定されたネットワークがホット スポット ネットワークを確認するには、この関数を呼び出します。 識別情報 (SSID、認証の種類、暗号) ネットワークを通過する[HS_NETWORK_IDENTITY](https://msdn.microsoft.com/library/windows/hardware/dn789356)構造体。 プラグインを返す必要があります、 [eHS_NETWORK_STATE](https://msdn.microsoft.com/library/windows/hardware/dn756756)ネットワークの種類を示す列挙値。 かどうかは、ホット スポット ネットワーク、ネットワークに関する情報がによって返される、 [HS_NETWORK_PROFILE](https://msdn.microsoft.com/library/windows/hardware/dn789357)構造体。 詳細については、次を参照してください。 [HS_PLUGIN_IS_HOTSPOT_NETWORK](https://msdn.microsoft.com/library/windows/hardware/dn789363)します。

### <a name="hspluginquerysupportedsims-optional"></a>HsPluginQuerySupportedSIMs [省略可能]

ホット スポットのプラグインのホストが、プラグインが機能を指定する場合、この関数を呼び出す**HS\_フラグ\_機能\_ネットワーク\_AUTH\_HTTP**または**HS\_フラグ\_機能\_ネットワーク\_AUTH\_EAP**で、 *HS_NETWORK_PROFILE* への呼び出しの引数[HS_PLUGIN_IS_HOTSPOT_NETWORK](https://msdn.microsoft.com/library/windows/hardware/dn789363)します。 PNetworkIdentity 引数が NULL 以外である必要がありますこのインスタンスで呼び出されると、およびプラグインが pNetworkIdentity のみで指定したネットワークのサポートされている Sim の一覧を提供する必要があります。 詳細については、次を参照してください。 [HS_PLUGIN_QUERY_SUPPORTED_SIMS](https://msdn.microsoft.com/library/windows/hardware/dn789368)します。

### <a name="hspluginquerycellularexceptionhosts-optional"></a>HSPluginQueryCellularExceptionHosts [省略可能]

ホット スポットのプラグインのホストがこの関数を呼び出す場合、 **dwNumCellularExceptions**のフィールド、 [HS_NETWORK_PROFILE](https://msdn.microsoft.com/library/windows/hardware/dn789357)プラグインによって返される構造は、0 以外の値に設定されます。 このプラグインは、呼び出されたときに、携帯電話のベアラー ホストの一覧を返す必要があります。 詳細については、次を参照してください。 [HS_PLUGIN_QUERY_CELLULAR_EXCEPTION_HOSTS](https://msdn.microsoft.com/library/windows/hardware/dn789366)します。

## <a name="connect-time"></a>接続時間

ネットワークは、接続可能と見なされます。 または、ユーザーが、ネットワークが選択されて、次の一連の呼び出しが行われます。

### <a name="hspluginpreconnectinit"></a>HSPluginPreConnectInit

ホット スポットのプラグインのホストでホット スポット ネットワークへの接続が指定されているプラグインを通知するには、この関数を呼び出し、 [HS_NETWORK_IDENTITY](https://msdn.microsoft.com/library/windows/hardware/dn789356)プラグインによって返される構造が進行中です。 詳細については、次を参照してください。 [HS_PLUGIN_PRE_CONNECT_INIT](https://msdn.microsoft.com/library/windows/hardware/dn789364)します。

### <a name="hspluginstartpostconnectauth"></a>HSPluginStartPostConnectAuth

L2 接続が完了したら、ホット スポットのプラグインのホストは、認証を開始するようにプラグインを通知するには、この関数を呼び出します。 プラグインが提供される、 *pConnectContext*、 *pNetworkIdentity*、および*pNetworkProfile*以前の呼び出しから**HSPluginPreConnectInit**も提供されますが、 *dwConnectionId*と*pSIMData*します。 プラグインが接続 ID を格納する必要がありますが、ホストのコールバック時に使用**HSHostPostConnectAuthCompletion**の認証の結果とへの呼び出しでも、OS に通知するハンドラー **HSHostSendUserMessage**メッセージがユーザーに伝える必要がある場合。 **PSIMData**構造体には、認証中にプラグインが必要でした SIM 構成に関する追加情報が含まれています。 呼び出す必要がありますが、プラグインでは、成功が返された場合**HSHostPostConnectAuthCompletion** 5 分以内の接続が切断されています。

## <a name="disconnect-and-reset"></a>切断し、リセット

一部のユーザーまたはデバイスのアクションによって明示的にまたは暗黙的に外部要因は、結果として、ネットワークが切断されたときに、次の関数が呼び出されます。

### <a name="hspluginstoppostconnectauth"></a>HSPluginStopPostConnectAuth

ホット スポットのプラグインのホストでは、デバイスは、ネットワークから切断されるため、ネットワーク認証を終了するには、この関数を呼び出します。 詳細については、次を参照してください。 [HS_PLUGIN_STOP_POST_CONNECT_AUTH](https://msdn.microsoft.com/library/windows/hardware/dn789372)します。

### <a name="hsplugindisconnectfromnetwork"></a>HSPluginDisconnectFromNetwork

ホット スポットのプラグインのホストでは、プラグイン、デバイスをネットワークから切断することを通知するためには、この関数を呼び出します。 詳細については、次を参照してください。 [HS_PLUGIN_DISCONNECT_FROM_NETWORK](https://msdn.microsoft.com/library/windows/hardware/dn789361)します。

### <a name="hspluginreset"></a>HSPluginReset

ホット スポットのプラグインのホストでは、プラグインを初期 (読み込んだ) 状態にリセットするには、この関数を呼び出します。 詳細については、次を参照してください。 [HS_PLUGIN_RESET](https://msdn.microsoft.com/library/windows/hardware/dn789369)します。

## <a name="periodic-calls"></a>定期的な呼び出し

特定のパラメーターが、プラグインによって設定に応じて、次の関数が、定期的に呼び出されます。

### <a name="hspluginsendkeepalive-optional"></a>HSPluginSendKeepAlive [省略可能]

ホット スポットのプラグインのホストで指定された頻度でこの関数を呼び出し、 **dwKeepAliveTimeMins**のメンバー、 [HS_NETWORK_PROFILE](https://msdn.microsoft.com/library/windows/hardware/dn789357)プラグインによって返される構造体。 詳細については、次を参照してください。 [HS_PLUGIN_SEND_KEEP_ALIVE](https://msdn.microsoft.com/library/windows/hardware/dn789370)します。

### <a name="hsplugincheckforupdates-optional"></a>HSPluginCheckForUpdates [省略可能]

ホット スポットのプラグインのホストで指定された頻度でこの関数を呼び出し、 **dwProfileUpdateTimeDays**のメンバー、 [HS_PLUGIN_PROFILE](https://msdn.microsoft.com/library/windows/hardware/dn789365)構造体。 

## <a name="unloading-the-plugin"></a>プラグインのアンロード

### <a name="hsplugindeinit"></a>HSPluginDeinit

ホット スポットのプラグインのホストでは、未保存のデータをフラッシュし、アンロードされる前に、開いているハンドルを終了するようにプラグインを有効にするには、この関数を呼び出します。 プラグインが理由でアンロードを指定する、 *UnloadReason*引数。 詳細については、次を参照してください。 [HS_PLUGIN_DEINIT](https://msdn.microsoft.com/library/windows/hardware/dn789360)します。

## <a name="plugin-installation-package"></a>プラグインのインストール パッケージ

プラグインのインストール パッケージは、次に示します。

### <a name="the-plugin-dll-file"></a>プラグインの DLL ファイル

DLL ファイルの署名し、の下に配置する必要があります**Programs\HotspotHost\\** <*ProviderName*> ここで、<*ProviderName*> は、DLL のプロバイダーの名前。 

DLL の署名については、次を参照してください。[バイナリとパッケージの署名](https://msdn.microsoft.com/library/windows/hardware/dn789217)します。 

必要なは、レジストリ、ファイルへのパスが正しいことを確認するため、DLL ファイルの名前付け規則を特定することはありません。 たとえば、パッケージにレジストリ情報を指定できました。

```xml
<RegKeys>
        <RegKey KeyName="$(hklm.software)\Microsoft\Windows Phone\HotspotOffload\Plugins\<ProviderName>">
          <RegValue Name="PluginRank" Type="REG_DWORD" Value="00000005" />
          <RegValue Name="PluginPath" Type="REG_SZ" Value="%SystemDrive%\Programs\HotspotHost\Orange\<ProviderName>\<HotspotPlugin.dll>" />
        </RegKey>
      </RegKeys>
```

### <a name="registry-configuration"></a>レジストリの構成

下に作成する新しいエントリには、必要なレジストリ設定が保存されます。**Hkey_local_machine \software\microsoft\windows Phone\HotspotOffload\Plugins\\**  *ProviderName*します。

*ProviderName*プラグインのプロバイダーまたはモバイル演算子に固有である必要があります。

レジストリ キーの下で、次の値を保存する必要があります。

| 名前 | 種類 | 説明 |
| --- | --- | --- |
| PluginPath | [REG_SZ] | 名前と、DLL への完全パス。 |
| PluginRank | [REG_DWORD] | 1 ~ 250、包括的で任意の正の値 (0 は Microsoft の予約済み)。 下限値より高い優先度を表します。 同じランクを 2 つのプラグインである場合、ホット スポット サービス任意を 1 つを優先します。 |

### <a name="data-files-that-contain-connection-specific-information-such-as-a-list-of-ssids-encrypted-credentials-etc-optional"></a>Ssid、暗号化された資格情報の一覧などの特定の接続情報を含むデータ ファイルなど [省略可能]

データ ファイルを保存する必要があります:`Data\SharedData\HotspotHost\Plugins\<ProviderName>`します。

