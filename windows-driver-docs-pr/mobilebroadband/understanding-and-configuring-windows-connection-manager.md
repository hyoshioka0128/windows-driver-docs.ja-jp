---
title: Windows 接続マネージャーの理解と構成
description: Windows 接続マネージャーの理解と構成
ms.assetid: 5ef0034f-5b30-4484-a11c-ed19931484a2
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 676d85427b41d04a3cea25356d41e233a354d8f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357938"
---
# <a name="understanding-and-configuring-windows-connection-manager"></a>Windows 接続マネージャーの理解と構成

> [!IMPORTANT]
> このトピックでは、Windows が自社のネットワークに接続する方法を構成できる Microsoft の通信事業者 (月) パートナー向けです。 Windows ネットワーク接続の問題が発生しているお客様の場合を参照してください。[で Windows ネットワーク接続の問題を修正](https://support.microsoft.com/help/10741/windows-fix-network-connection-issues)します。

自動接続管理、Windows 8 で導入されたは、イーサネット、Wi-fi、およびモバイル ブロード バンド インターフェイスを調べることで、接続の決定を行います。 これらの決定のリードを 自動接続し、Wi-fi とモバイル ブロード バンド インターフェイスにアクションを切断します。

> [!NOTE]
> Windows では、イーサネット接続に応答しは、イーサネット接続を自動的に管理しません。

このトピックでは、方法 Windows 自動的に物理のワイヤレス接続を管理し、これらの接続を考慮しませんについて説明します。

-   ダイヤルアップ接続、モデムなど

-   Vpn トンネルの接続の IP などの純粋仮想インターフェイス

## <a name="span-idconnectionmanagementpoliciesspanspan-idconnectionmanagementpoliciesspanspan-idconnectionmanagementpoliciesspanconnection-management-policies"></a><span id="Connection_management_policies"></span><span id="connection_management_policies"></span><span id="CONNECTION_MANAGEMENT_POLICIES"></span>接続の管理ポリシー

Windows 8、Windows 8.1、および Windows 10 には、多く接続を管理するポリシーにはが含まれます。 これらのポリシーは、Windows ユーザー インターフェイスで公開されないを使用して構成することができます、 [WcmSetProperty](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetproperty) API またはグループ ポリシー。

### <a name="span-idminimizesimultaneousconnectionsspanspan-idminimizesimultaneousconnectionsspanspan-idminimizesimultaneousconnectionsspanminimize-simultaneous-connections"></a><span id="Minimize_simultaneous_connections"></span><span id="minimize_simultaneous_connections"></span><span id="MINIMIZE_SIMULTANEOUS_CONNECTIONS"></span>同時接続を最小限に抑える

このポリシーを構成を使用して、 **fMinimizeConnections**グループ ポリシー。 Windows 8、Windows 8.1、および Windows 10 の既定ではオンです。

#### <a name="versions-of-windows-before-windows-10-version-1809-build-17763404"></a>Windows 10、バージョンは 1809 より前に、の Windows のバージョンで 17763.404 をビルドします。

Windows 8、Windows 8.1、および Windows 10、バージョンは 1809、17763.404、ビルドする前に Windows 10 のバージョンでこのポリシーは、いずれかのグループ ポリシーを使用して変更可能なブール値、または[WcmSetProperty](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetproperty) API。

このポリシーが無効になっている場合、動作は他のインターフェイスの接続状態に関係なく、範囲内で最も優先度のネットワークに接続する各インターフェイスを Windows 7 と同様にします。

このポリシーを有効にすると、Windows は最適に利用可能なレベルの接続を提供する同時接続の最小数を維持しようとします。 Windows では、次のネットワークへの接続を保持します。

-   任意のイーサネット ネットワーク

-   現在のユーザー セッション中に手動で接続されているすべてのネットワーク

-   インターネットへの接続を最も優先度

-   PC がドメインに参加している場合、Active Directory ドメインへの接続を最も優先度

残りのすべてのネットワークは論理的な-切断、ように、次のセクションで説明されています。 これは、接続されていない使用可能なネットワークの評価にも使用します。 Windows は、元となることがすぐに論理的な切断の新しいネットワークに接続できません。

#### <a name="windows-10-version-1809-build-17763404-and-later"></a>Windows 10、バージョンは 1809、17763.404 およびそれ以降のビルド

Windows 10、バージョンは 1809、17763.404 以降のビルドでは、この値はのみグループ ポリシーで使用可能な列挙体です。

このポリシー設定は、コンピューターがインターネット、Windows ドメイン、または両方に複数の接続を持つことができるかどうかを決定します。 複数の接続が許可されている場合、ポリシーがネットワーク トラフィックをルーティングする方法を決定します。

このポリシーに設定されている場合**0**コンピューターがインターネット、Windows ドメイン、または両方を同時接続を持つことができます。 携帯ネットワーク接続または任意の従量制課金接続を含む、任意の接続経由でインターネット トラフィックをルーティングできます。 これは以前、*無効*Windows 10、バージョンは 1809、17663.404 をビルドする前に、Windows のビルドでは、このポリシー設定の状態。 このオプションで初めて提供された Windows 8。

このポリシーに設定されている場合**1**、任意の新しい自動インターネット接続がブロックされているコンピューターに推奨される種類のネットワークに少なくとも 1 つのアクティブなインターネット接続がある場合。 優先順位は次のとおりです。

1. Ethernet
2. WLAN
3. Cellular

イーサネットは接続されているときに常に優先します。 ユーザーは、どのネットワークに手動で接続できます。 これは以前、*有効*Windows 10、バージョンは 1809、17763.404 をビルドする前に、Windows のビルドでは、このポリシー設定の状態。 このオプションで初めて提供された Windows 8。

このポリシー設定設定されている場合**2**、動作に似ていますがこれに設定すると**1**します。 ただし、携帯データ ネットワーク接続を使用できる場合、その接続は常に、携帯ネットワーク接続を必要とするサービスに接続されたままです。 ユーザーが、VLAN、またはイーサネット接続に接続されている場合は、携帯ネットワーク接続経由でにインターネット トラフィックはルーティングされません。 このオプションは、Windows 10 バージョン 1703 で使用可能な初めてされました。

このポリシー設定設定されている場合**3**、動作設定されている場合に似ています**2**します。 ただし、イーサネット接続がある場合は、Windows は、WLAN に手動で接続するユーザーは許可されていません。 WLAN のみ接続できます (自動または手動で) とイーサネット接続ではありません。

### <a name="span-idsoftdisconnectspanspan-idsoftdisconnectspanspan-idsoftdisconnectspansoft-disconnect"></a><span id="Soft_disconnect"></span><span id="soft_disconnect"></span><span id="SOFT_DISCONNECT"></span>論理的な切断します。

論理的な切断は次のように動作します。

1.  Windows では、ネットワークが接続されなくなります。 を決定したら、そのすぐに切断されません。 突然切断ほどの利点を提供することがなく、ユーザー エクスペリエンスが低下して、可能な限り回避されます。

2.  Windows では、インターフェイスを論理的な切断をすぐに通知 TCP スタック、ネットワークが使用できなくする必要があります。 既存の TCP セッションが中断なく続行が新しい TCP セッションが場合にのみ、このインターフェイスを明示的に使用、バインドまたは目的の転送先にその他のインターフェイスをルーティングしないかどうか。

3.  TCP スタックには、この通知は、ネットワーク状態の変更を生成します。 ネットワーク アプリケーションは、これらのイベントをリッスンし、事前に可能であれば、接続を新しいネットワークに移動する必要があります。

4.  30 秒ごとと、Windows では、インターフェイスのトラフィックのレベルが確認されます。 トラフィック レベルは、特定のしきい値を超えていますが場合、これ以上の操作は行われません。 これによりなど、ファイル転送や中断を回避するために、VoIP 呼び出しから、継続的なインターフェイスの使用ができます。

5.  トラフィックがこのしきい値を下回ったときに、インターフェイスは切断されます。 電子メール クライアントなどの有効期間が長いアイドル接続を保持するアプリケーションでは、中断する可能性があり、別のインターフェイス経由で接続を再確立する必要があります。

### <a name="span-idinitialconnectionspanspan-idinitialconnectionspanspan-idinitialconnectionspaninitial-connection"></a><span id="Initial_connection"></span><span id="initial_connection"></span><span id="INITIAL_CONNECTION"></span>最初の接続

Windows は自動的に接続するとすぐに論理的な-接続を切断し 1 つの状況で。 PC が初めて起動したり、スタンバイから再開、ときに、すべてのインターフェイスは同時に、ユーザーは、可能な限り早くにネットワーク接続を取得することを確認するには接続を試みます。 複数のインターフェイスは正常に接続する場合は、Windows がすぐにインターフェイスを論理的な切断を開始します。

### <a name="span-idprohibitinterconnectbetweendomainandnon-domainnetworksspanspan-idprohibitinterconnectbetweendomainandnon-domainnetworksspanspan-idprohibitinterconnectbetweendomainandnon-domainnetworksspanprohibit-interconnect-between-domain-and-non-domain-networks"></a><span id="Prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="PROHIBIT_INTERCONNECT_BETWEEN_DOMAIN_AND_NON-DOMAIN_NETWORKS"></span>禁止のドメインと非ドメイン ネットワーク間の相互接続

このポリシーは Windows 8、Windows 8.1、および Windows 10 の既定で無効にします。 このポリシーを有効にすると、Windows PC がドメイン ネットワークと非ドメイン ネットワーク間で相互に接続されていることを防止しようとします。 攻撃ポイントとして、マルチホーム コンピューターを使用してセキュリティ侵害の可能性を懸念される場合は、エンタープライズ管理者でこれを使用できます。

すべてのネットワーク ルートをドメインに接続したり、ドメインに接続されたネットワーク ルート操作を実行すると、このポリシーでは、このシステムの動作は影響しません。

### <a name="span-idmultiplewirelessnetworksspanspan-idmultiplewirelessnetworksspanspan-idmultiplewirelessnetworksspanmultiple-wireless-networks"></a><span id="Multiple_wireless_networks"></span><span id="multiple_wireless_networks"></span><span id="MULTIPLE_WIRELESS_NETWORKS"></span>複数のワイヤレス ネットワーク

多くの Windows 8、Windows 8.1、または Windows 10 モバイル デバイスは、外部のインターネット接続を利用することを常に、企業の Wi-fi ネットワークの範囲にある場合でも必要があります。 このポリシーを有効にすると、ユーザーことがあります自由にいずれかに、パブリックのモバイル ブロード バンド ネットワークまたは接続を企業のプライベート Wi-fi ネットワークとスイッチでそれらの間にはします。 ただし、手動で 1 つの接続は自動的に、すぐに切断するその他。

### <a name="span-idethernetspanspan-idethernetspanspan-idethernetspanethernet"></a><span id="Ethernet"></span><span id="ethernet"></span><span id="ETHERNET"></span>イーサネット

Windows 8、Windows 8.1、または Windows 10 に自動的に接続または実行できないため、PC にイーサネット ケーブルの切断、ことのみを許可またはワイヤレス接続を禁止することによってポリシーを適用することができます。 PC がドメイン ネットワークへのイーサネット接続の場合、ドメインに接続していないワイヤレス ネットワークを接続することはできません、またはその逆です。 試行を行うには、次のエラーになります。

![自動接続管理エラー](images/mb-acm-1.png)

複数のイーサネット ポートがある Pc、Windows は異なる 2 つのイーサネット ネットワークに、PC を物理的に接続することによって作成される相互接続を防ぐことはできません。

### <a name="span-ideffectonsoftdisconnectspanspan-ideffectonsoftdisconnectspanspan-ideffectonsoftdisconnectspaneffect-on-soft-disconnect"></a><span id="Effect_on_soft_disconnect"></span><span id="effect_on_soft_disconnect"></span><span id="EFFECT_ON_SOFT_DISCONNECT"></span>論理的なへの影響を切断します。

相互接続を禁止することがセキュリティの考慮事項のため、このポリシーに準拠している任意の切断すぐ、進行中のアクティビティがある場合でもです。 ユーザーは中断が発生する接続ネットワークと企業ネットワークの間で遷移するときに、2 つのネットワークが重複している場合でもです。

たとえば、企業のイーサネット接続にドッキングされているラップトップをモバイル ブロード バンド ネットワーク経由での VoIP 通話に携わるユーザーでは、アプリが新しい接続経由で自動的に回復することができますが、呼び出しが失われます。 ポリシーが有効でない場合 Windows は代わりに論理的な - モバイル ブロード バンド接続して切断呼び出しが完了するを待ちます。 その一方で、両方のネットワークがドメインに接続するために、企業ネットワークにドッキングされているとき、企業の Wi-fi ネットワーク経由で開始 VoIP 呼び出しは中断されません。 Wi-fi ネットワークは、呼び出しの完了後に切断されます。

### <a name="span-idprohibitroamingonmobilebroadbandnetworksspanspan-idprohibitroamingonmobilebroadbandnetworksspanspan-idprohibitroamingonmobilebroadbandnetworksspanprohibit-roaming-on-mobile-broadband-networks"></a><span id="Prohibit_roaming_on_mobile_broadband_networks"></span><span id="prohibit_roaming_on_mobile_broadband_networks"></span><span id="PROHIBIT_ROAMING_ON_MOBILE_BROADBAND_NETWORKS"></span>モバイル ブロード バンド ネットワークでローミングを禁止します。

このポリシーでは、Windows がローミングの状態にあるモバイル ブロード バンド ネットワークに接続できなくなります。 既定では、このポリシーが無効になっているし、ユーザーは、手動でローミング中に、モバイル ブロード バンド ネットワークに接続するか、自動的にこのようなネットワークへの接続を有効にするを選択できます。 ユーザーが有効な場合は、ローミング モバイル ブロード バンド ネットワークが接続マネージャーからに選択できません。

## <a name="span-idnetworkpreferencesspanspan-idnetworkpreferencesspanspan-idnetworkpreferencesspannetwork-preferences"></a><span id="Network_preferences"></span><span id="network_preferences"></span><span id="NETWORK_PREFERENCES"></span>ネットワーク環境設定


維持するために複数の接続を検討して、Windows は、優先するネットワークを決定するのに特徴の数を使用します。 これは、ルーティングではなく、特定のインターフェイスへの接続を維持するかどうかを決定するときにのみ使用されます。 プロセスに接続されているインターフェイスがない場合は、接続が切断されるソフト、ルーティングはルーティング テーブルに表示されるメトリックによって決定されます。 ルートのメトリックが手動で指定されていない場合は、Windows はアダプターのリンク速度に基づいてルートのメトリックを自動的に割り当てます。

### <a name="span-idconnectionprioritiesspanspan-idconnectionprioritiesspanspan-idconnectionprioritiesspanconnection-priorities"></a><span id="Connection_priorities"></span><span id="connection_priorities"></span><span id="CONNECTION_PRIORITIES"></span>接続の優先順位

Windows では、次の順序で接続を優先します。

1.  イーサネット ネットワーク

2.  現在のユーザー セッション中に手動で接続されているネットワーク

3.  インターネットと、PC が参加している Active Directory ドメインの両方に接続するネットワーク

4.  現在接続している Wi-fi ネットワークの信号強度

5.  PC の優先ネットワーク一覧

リンク速度は、現在接続されているインターフェイスの間でのルーティングの動作に影響を場合でも、Windows はリンク速度や、ネットワークのスループットに基づいて接続の決定を行いません。 モバイル ブロード バンド ネットワークと、モバイル ブロード バンド ネットワークの現在の速度に基づいて Wi-fi ネットワークの間の接続設定を変更する Windows を構成することはできません。 両方が接続されている場合、ユーザーまたはデスクトップ アプリはルートのメトリックに影響を与えるルーティング設定を変更できます。

### <a name="span-idsignalstrengthspanspan-idsignalstrengthspanspan-idsignalstrengthspansignal-strength"></a><span id="Signal_strength"></span><span id="signal_strength"></span><span id="SIGNAL_STRENGTH"></span>信号の強度

Windows では、現在接続している Wi-fi ネットワークに非常に低い信号の強さを検出する場合にネットワーク接続の中断を回避する (ポリシーによって許可されている) 場合、モバイル ブロード バンド ネットワークに接続できます。 これにより、ユーザーがワイヤレス アクセス ポイントから移動するときに、移行を滑らかにします。

Windows では、信号の強さは、接続を維持できないまでより優先される Wi-fi ネットワークを切断しません。 信号強度が向上しますが場合、Windows 可能性がありますソフト - アダプターを取り外しますモバイル ブロード バンド。

### <a name="span-idpreferrednetworklistspanspan-idpreferrednetworklistspanspan-idpreferrednetworklistspanpreferred-network-list"></a><span id="Preferred_network_list"></span><span id="preferred_network_list"></span><span id="PREFERRED_NETWORK_LIST"></span>優先ネットワーク一覧

ほとんどの場合は、優先ネットワーク一覧は、Windows を使用して接続するワイヤレス ネットワーク プロファイルを決定します。 前の Windows 8 では、この一覧の Wi-fi ネットワークをのみに適用します。 Windows 8、Windows 8.1、および Windows 10 でのモバイル ブロード バンド ネットワークを含めることもできます。

### <a name="span-idautomaticgenerationspanspan-idautomaticgenerationspanspan-idautomaticgenerationspanautomatic-generation"></a><span id="Automatic_generation"></span><span id="automatic_generation"></span><span id="AUTOMATIC_GENERATION"></span>自動生成

Windows 8、Windows 8.1、および Windows 10 は、ユーザーのアクションに基づいて優先ネットワーク一覧を自動的に更新します。 任意の手動接続または切断は、将来的に同じ動作が自動的に発生するように、ネットワークの一覧を更新します。

次のユーザー操作は、優先ネットワーク一覧を変更します。

-   **最初に接続するネットワーク**新しいネットワークがネットワークの一覧に追加されます。 ユーザーは、ネットワークにより、将来自動的に接続するかどうかを指定します。

    -   最初に新しい Wi-fi ネットワークに接続する、ネットワーク、最も優先度のネットワークの一覧でします。

    -   最初に、新しいモバイル ブロード バンド ネットワークに接続するは、ネットワーク、最小限の推奨されるネットワーク内のリスト。

-   **手動での Wi-fi ネットワークに接続**一覧の上の範囲内の他の Wi-fi ネットワークは、新しく接続したネットワークの一覧で下に移動されます。 ユーザーは、かどうか、ネットワークに自動的に接続、将来を指定します。

-   **ネットワークから切断する**Windows が自動的にネットワークに接続できないこの将来します。 場合は、ユーザーが、今後、この設定を変更するネットワークの一覧に残ります。

### <a name="span-idgrouppolicyspanspan-idgrouppolicyspanspan-idgrouppolicyspangroup-policy"></a><span id="Group_Policy"></span><span id="group_policy"></span><span id="GROUP_POLICY"></span>グループ ポリシー

グループ ポリシーによって作成された Wi-fi プロファイルでは、ネットワークの一覧の上部にあります。 ユーザーが手動でこれらのネットワークから切断または手動で他のネットワークに接続しますが、これらのネットワークは、グループ ポリシーによって削除されるまで、ネットワークの一覧の最上位の位置に残ります。

### <a name="span-idcarrier-provisioningmetadataspanspan-idcarrier-provisioningmetadataspanspan-idcarrier-provisioningmetadataspancarrier-provisioning-metadata"></a><span id="Carrier-provisioning_metadata"></span><span id="carrier-provisioning_metadata"></span><span id="CARRIER-PROVISIONING_METADATA"></span>通信事業者のプロビジョニングのメタデータ

モバイル ブロード バンド接続と Wi-fi ホット スポット提供事業者向け Windows 一連のモバイル ブロード バンド接続と Wi-fi プロファイルを使用して提供、 [ **ProvisioningAgent** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)または[ **msProvisionNetworks** ](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) Api。

最初にプロビジョニングすると、演算子が作成したプロファイルは、上部 (Wi-fi のみ) または既存のネットワークの一覧の下部 (モバイル ブロード バンドが含まれる場合) に追加されます。 ネットワークの一覧にプロビジョニングするネットワークの位置の影響を与えることはできません。 ただし、ネットワークの一覧で、自社のネットワークの相対順序を定義できます。

ユーザーの操作には、メタデータのプロビジョニングのアプリケーション間でネットワークの一覧を変更できます。 プロビジョニングのメタデータを適用し、目的のネットワークの注文が復元されます。 ただし、ネットワークの並べ替えられたセットは、移動先となる、ユーザーが、ネットワークのいずれかの最下位の位置に移動されます。

プロビジョニングのメタデータでのネットワーク間の基本設定は、次のように決定されます。

1.  ネットワーク プロファイルごとにオプションの優先順位属性

2.  メディアの種類 (Wi-fi はモバイル ブロード バンドよりもより優先される)

3.  XML ファイルで指定された順序

### <a name="span-idmanualmodificationspanspan-idmanualmodificationspanspan-idmanualmodificationspanmanual-modification"></a><span id="Manual_modification"></span><span id="manual_modification"></span><span id="MANUAL_MODIFICATION"></span>手動の変更

Windows 8 の前に、Wi-fi で優先ネットワーク一覧されたワイヤレス ネットワークの管理コントロール パネルからユーザーがアクセスできます。 製品利用統計情報は、ごく限られたユーザーは、この機能をこれまでアクセスを示します。 さらに、このユーザー インターフェイスは Wi-fi にのみ関連付けられたし、Wi-fi とモバイル ブロード バンドの間の基本設定を組み込んでいない可能性があります。

ほとんどのユーザーは、ネットワークの一覧を手動で変更する必要はありません。 ただし、特定のユーザーまたはアプリケーション必要があるようにします。

### <a name="span-iduserinterfacespanspan-iduserinterfacespanspan-iduserinterfacespanuser-interface"></a><span id="User_interface"></span><span id="user_interface"></span><span id="USER_INTERFACE"></span>ユーザー インターフェイス

範囲内にあるときに、優先ネットワーク一覧からプロファイルを削除して、ネットワークを右クリックし、選択**このネットワークもご活用ください**します。 範囲に含まれていないネットワークは、ユーザー インターフェイスを通じてリストから削除できません。

### <a name="span-idwin32apisspanspan-idwin32apisspanspan-idwin32apisspanwin32-apis"></a><span id="Win32_APIs"></span><span id="win32_apis"></span><span id="WIN32_APIS"></span>Win32 Api

アプリケーションは、適切なメディア固有 API を使用してネットワークの一覧に新しいプロファイルを作成することがあります。

-   Wi-fi ネットワークを使用して、 [ **WlanSetProfile** ](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlansetprofile)関数。

-   モバイル ブロード バンド ネットワークを使用して、 [ **IMbnConnectionProfileManager::CreateConnectionProfile** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionprofilemanager-createconnectionprofile)メソッド。

ネットワークの一覧の順序を変更するには、使用、 [ **WcmSetProfileList** ](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetprofilelist)関数。 使用しないで、 [ **WlanSetProfileList** ](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlansetprofilelist)関数を予想外の方法でモバイル ブロード バンドのプロファイルのネットワークの一覧内の位置を妨害する可能性があります。

ネットワークの一覧からプロファイルを削除するには、適切なメディア固有 API を使用します。

-   Wi-fi ネットワークを使用して、 [ **WlanDeleteProfile** ](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlandeleteprofile)関数。

-   モバイル ブロード バンド ネットワークを使用して、 [ **IMbnConnectionProfile::Delete** ](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionprofile-delete)メソッド。

### <a name="span-idcommand-linespanspan-idcommand-linespanspan-idcommand-linespancommand-line"></a><span id="Command-line"></span><span id="command-line"></span><span id="COMMAND-LINE"></span>コマンド ライン

ユーザーまたはスクリプトは、適切なメディアに固有のコマンドを使用して新しいプロファイルをネットワークの一覧に作成可能性があります。

-   Wi-fi ネットワークを使用して、 **netsh wlan は、プロファイルを追加**コマンド。

-   モバイル ブロード バンド ネットワークを使用して、 **netsh mbn プロファイルを追加する**コマンド。

使用して、ネットワークの一覧で、Wi-fi プロファイルの順序を変更する可能性があります、 **netsh wlan 設定 profileorder**コマンド。 ただし、これは使用しないで、予想外の方法でモバイル ブロード バンドのプロファイルのリスト内の位置を妨害することができます。

ネットワークの一覧からプロファイルを削除するには、適切なメディアに固有のコマンドを使用します。

-   Wi-fi ネットワークを使用して、 **netsh wlan は、プロファイルを削除する**コマンド。

-   モバイル ブロード バンド ネットワークを使用して、 **netsh mbn プロファイルを削除する**コマンド。

### <a name="span-idconflictresolutionspanspan-idconflictresolutionspanspan-idconflictresolutionspanconflict-resolution"></a><span id="Conflict_resolution"></span><span id="conflict_resolution"></span><span id="CONFLICT_RESOLUTION"></span>競合の解決

複数のプロファイルは、同じネットワークに存在する場合 Windows 8 および Windows 8.1 を使用して、次のロジックを決定するプロファイルを使用する必要があります。

1.  **プロファイルの種類**

    1.  グループ ポリシー プロファイルは、ユーザーが作成したプロファイルより優先されます。

    2.  すべてのユーザー プロファイルは、シングル ユーザー プロファイルを優先します。

2.  **インターフェイスの到着**最近インストールされたインターフェイスでプロファイルが使用されます。

 

 





