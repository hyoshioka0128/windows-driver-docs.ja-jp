---
title: Windows 接続マネージャーの理解と構成
description: Windows 接続マネージャーの理解と構成
ms.assetid: 5ef0034f-5b30-4484-a11c-ed19931484a2
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0046844b912bdaebb3766d188bbf3383a7adf4fa
ms.sourcegitcommit: bd120d96651f9e338956388c618acec7d215b0d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681680"
---
# <a name="understanding-and-configuring-windows-connection-manager"></a>Windows 接続マネージャーの理解と構成

> [!IMPORTANT]
> このトピックは、Windows がネットワークに接続する方法を構成できる Microsoft の携帯電話 (MO) パートナーを対象としています。 Windows ネットワーク接続の問題が発生しているお客様の場合は、「 [windows でのネットワーク接続の問題の修正](https://support.microsoft.com/help/10741/windows-fix-network-connection-issues)」を参照してください。

Windows 8 で導入された自動接続管理は、イーサネット、Wi-fi、およびモバイルブロードバンドインターフェイスを調べることによって、接続の決定を行います。 これらの決定は、Wi-fi およびモバイルブロードバンドインターフェイスでの自動接続と切断操作につながります。

> [!NOTE]
> Windows はイーサネット接続に応答しますが、イーサネット接続は自動的には管理されません。

このトピックでは、Windows が物理的なワイヤレス接続を自動的に管理する方法と、これらの接続を考慮しない方法について説明します。

-   モデムなどのダイヤルアップ接続

-   純粋仮想インターフェイス (Vpn、トンネル IP 接続など)

## <a name="span-idconnection_management_policiesspanspan-idconnection_management_policiesspanspan-idconnection_management_policiesspanconnection-management-policies"></a><span id="Connection_management_policies"></span><span id="connection_management_policies"></span><span id="CONNECTION_MANAGEMENT_POLICIES"></span>接続管理ポリシー

Windows 8、Windows 8.1、Windows 10 には、接続管理を制御するための多数のポリシーが含まれています。 これらのポリシーは Windows ユーザーインターフェイスでは公開されませんが、 [Wcmsetproperty](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetproperty) API またはグループポリシーを使用して構成できます。

### <a name="span-idminimize_simultaneous_connectionsspanspan-idminimize_simultaneous_connectionsspanspan-idminimize_simultaneous_connectionsspanminimize-simultaneous-connections"></a><span id="Minimize_simultaneous_connections"></span><span id="minimize_simultaneous_connections"></span><span id="MINIMIZE_SIMULTANEOUS_CONNECTIONS"></span>同時接続を最小化する

このポリシーは、 **fMinimizeConnections**グループポリシーを使用して構成されます。 Windows 8、Windows 8.1、および Windows 10 では既定でオンになっています。

#### <a name="versions-of-windows-before-windows-10-version-1809-build-17763404"></a>Windows 10、バージョン1809、ビルド17763.404 より前の Windows のバージョン

Windows 8、Windows 8.1、windows 10 のバージョン1809、ビルド17763.404 より前のバージョンでは、このポリシーはグループポリシーまたは[Wcmsetproperty](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetproperty) API を使用して変更できるブール値です。

このポリシーが無効になっている場合、この動作は、他のインターフェイスの接続状態に関係なく、各インターフェイスが範囲内の最も優先されるネットワークに接続する Windows 7 の動作に似ています。

このポリシーが有効になっている場合、Windows は、使用可能な最高レベルの接続を提供する最小数の同時接続を維持しようとします。 Windows は、次のネットワークへの接続を維持します。

-   任意のイーサネットネットワーク

-   現在のユーザーセッション中に手動で接続されたすべてのネットワーク

-   インターネットに最も適した接続

-   PC がドメインに参加している場合に Active Directory ドメインに最も優先的に接続する

残りのすべてのネットワークは、次のセクションで説明するように、ソフト接続解除されます。 これは、接続されていない使用可能なネットワークの評価にも使用されます。 Windows は、すぐにソフト接続を解除する新しいネットワークには接続しません。

#### <a name="windows-10-version-1809-build-17763404-and-later"></a>Windows 10 バージョン1809、ビルド17763.404 以降

Windows 10 バージョン1809、ビルド17763.404 以降では、この値はグループポリシーを通じてのみ使用できる列挙体です。

このポリシー設定は、コンピューターがインターネット、Windows ドメイン、またはその両方に対して複数の接続を持つことができるかどうかを決定します。 複数の接続が許可されている場合、ポリシーはネットワークトラフィックをルーティングする方法を決定します。

このポリシーが**0**に設定されている場合、コンピューターはインターネット、Windows ドメイン、またはその両方への同時接続を持つことができます。 インターネットトラフィックは、携帯電話接続や従量制課金ネットワークなど、任意の接続を介してルーティングできます。 以前は、windows 10 バージョン1809、ビルド17663.404 より前の Windows のビルドでは、このポリシー設定の*無効*な状態でした。 このオプションは、Windows 8 で最初に使用できました。

このポリシーが**1**に設定されている場合、コンピューターが、優先するネットワークに対して少なくとも1つのアクティブなインターネット接続を使用していると、新しい自動インターネット接続はブロックされます。 優先順位は次のとおりです。

1. イーサネット
2. WLAN
3. 移動体通信

接続されている場合は、常にイーサネットが優先されます。 ユーザーは、引き続き任意のネットワークに手動で接続できます。 これは、Windows 10 バージョン1809、ビルド17763.404 より前の Windows のビルドで、このポリシー設定の [*有効*] 状態でした。 このオプションは、Windows 8 で最初に使用できました。

このポリシー設定が**2**に設定されている場合、の動作は、 **1**に設定されている場合と似ています。 ただし、携帯データネットワーク接続が使用可能な場合、その接続は常に携帯電話接続を必要とするサービスに対して接続されたままになります。 ユーザーが WLAN またはイーサネット接続に接続されている場合、インターネットトラフィックは携帯ネットワーク接続を経由してルーティングされません。 このオプションは、Windows 10 バージョン1703で初めて使用できました。

このポリシー設定が**3**に設定されている場合、この動作は**2**に設定されている場合と似ています。 ただし、イーサネット接続がある場合、Windows では、ユーザーが WLAN に手動で接続することを許可していません。 WLAN は、イーサネット接続がない場合にのみ接続できます (自動または手動)。

### <a name="span-idsoft_disconnectspanspan-idsoft_disconnectspanspan-idsoft_disconnectspansoft-disconnect"></a><span id="Soft_disconnect"></span><span id="soft_disconnect"></span><span id="SOFT_DISCONNECT"></span>ソフト切断

ソフト切断ポリシーは、次のように機能します。

1.  ネットワークが接続されなくなったと判断された場合、直ちに切断されることはありません。 突然の切断は、ほどの特典を提供することなくユーザーエクスペリエンスを低下させ、可能な限り回避します。

2.  Windows によってインターフェイスのソフト切断が決定されるとすぐに、ネットワークが使用されなくなることが TCP スタックに通知されます。 既存の TCP セッションは中断せずに続行されますが、新しい TCP セッションでは、明示的にバインドされている場合、または目的の宛先に他のインターフェイスがルーティングされない場合にのみ、このインターフェイスが使用されます。

3.  TCP スタックへのこの通知によって、ネットワークの状態の変更が生成されます。 ネットワークアプリケーションは、可能であれば、これらのイベントをリッスンし、新しいネットワークに事前に接続を移動する必要があります。

4.  次に、Windows は、インターフェイスのトラフィックレベルを30秒ごとに確認します。 トラフィックレベルが特定のしきい値を超えている場合は、これ以上の操作は実行されません。 これにより、ファイル転送や VoIP 呼び出しなど、中断を回避するために、インターフェイスを継続的に使用できるようになります。

5.  トラフィックがこのしきい値を下回ると、インターフェイスは切断されます。 電子メールクライアントなど、有効期間が長いアイドル状態の接続を保持するアプリケーションは中断される可能性があり、別のインターフェイスを介して接続を再確立する必要があります。

### <a name="span-idinitial_connectionspanspan-idinitial_connectionspanspan-idinitial_connectionspaninitial-connection"></a><span id="Initial_connection"></span><span id="initial_connection"></span><span id="INITIAL_CONNECTION"></span>初期接続

Windows は自動的に接続し、1つの状況ですぐにソフト切断します。 PC を初めて起動するか、スタンバイから再開すると、すべてのインターフェイスが同時に接続を試行し、ユーザーができるだけ迅速にネットワーク接続を取得できるようにします。 複数のインターフェイスが正常に接続されている場合、Windows はすぐにソフト切断インターフェイスを開始します。

### <a name="span-idprohibit_interconnect_between_domain_and_non-domain_networksspanspan-idprohibit_interconnect_between_domain_and_non-domain_networksspanspan-idprohibit_interconnect_between_domain_and_non-domain_networksspanprohibit-interconnect-between-domain-and-non-domain-networks"></a><span id="Prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="prohibit_interconnect_between_domain_and_non-domain_networks"></span><span id="PROHIBIT_INTERCONNECT_BETWEEN_DOMAIN_AND_NON-DOMAIN_NETWORKS"></span>ドメインとドメイン以外のネットワーク間の相互接続を禁止する

このポリシーは、Windows 8、Windows 8.1、および Windows 10 では既定で無効になっています。 このポリシーを有効にすると、Windows は、ドメインネットワークとドメイン以外のネットワークとの間で PC が相互接続されないようにします。 企業の管理者は、マルチホームコンピューターを攻撃ポイントとして使用することによって潜在的なセキュリティ違反を懸念する場合に、これを使用できます。

このポリシーは、接続されているすべてのネットワークがドメインにルーティングされる場合、またはドメインに接続されているネットワークルートがない場合に、システムの動作に影響しません。

### <a name="span-idmultiple_wireless_networksspanspan-idmultiple_wireless_networksspanspan-idmultiple_wireless_networksspanmultiple-wireless-networks"></a><span id="Multiple_wireless_networks"></span><span id="multiple_wireless_networks"></span><span id="MULTIPLE_WIRELESS_NETWORKS"></span>複数のワイヤレスネットワーク

多くの Windows 8、Windows 8.1、および Windows 10 mobile デバイスは、エンタープライズ Wi-fi ネットワークの範囲内であっても、常に外部インターネット接続を利用できます。 このポリシーが有効になっている場合、ユーザーは、パブリックモバイルブロードバンドネットワークまたは企業のプライベート Wi-fi ネットワークに自由に接続し、それらを自由に切り替えることができます。 ただし、手動で接続すると、もう一方が自動的に切断されます。

### <a name="span-idethernetspanspan-idethernetspanspan-idethernetspanethernet"></a><span id="Ethernet"></span><span id="ethernet"></span><span id="ETHERNET"></span>ビット

Windows 8、Windows 8.1、および Windows 10 は、イーサネットケーブルを PC に自動的に接続または切断することができないため、ワイヤレス接続を許可または禁止することによってのみ、ポリシーを適用できます。 PC にドメインネットワークへのイーサネット接続がある場合、そのドメインに接続していないワイヤレスネットワークを接続することはできません。その逆も同様です。 これを行おうとすると、次のエラーが発生します。

![自動接続管理エラー](images/mb-acm-1.png)

複数のイーサネットポートがある Pc の場合、Windows では、PC を2つの異なるイーサネットネットワークに物理的に接続することによって作成された相互接続を防ぐことはできません。

### <a name="span-ideffect_on_soft_disconnectspanspan-ideffect_on_soft_disconnectspanspan-ideffect_on_soft_disconnectspaneffect-on-soft-disconnect"></a><span id="Effect_on_soft_disconnect"></span><span id="effect_on_soft_disconnect"></span><span id="EFFECT_ON_SOFT_DISCONNECT"></span>ソフト切断への影響

相互接続の禁止はセキュリティ上の考慮事項であるため、このポリシーに準拠している切断は、進行中のアクティビティがある場合でも直ちに有効になります。 2つのネットワークが重複する場合でも、ユーザーは、パブリックネットワークと企業ネットワークの間を移行するときに接続が中断されます。

たとえば、会社のイーサネット接続に装着されているラップトップを使用してモバイルブロードバンドネットワーク経由での VoIP 通話を行うユーザーは、新しい接続を介して自動的に回復できる場合がありますが、通話は失われます。 ポリシーが有効になっていない場合、Windows は、呼び出しが完了するまで待機することによって、モバイルブロードバンド接続をソフト切断します。 一方、企業の Wi-fi ネットワーク経由で開始される VoIP 通話は、両方のネットワークがドメインに接続するため、企業ネットワークにドッキングしても中断されません。 呼び出しが完了すると、Wi-fi ネットワークが切断されます。

### <a name="span-idprohibit_roaming_on_mobile_broadband_networksspanspan-idprohibit_roaming_on_mobile_broadband_networksspanspan-idprohibit_roaming_on_mobile_broadband_networksspanprohibit-roaming-on-mobile-broadband-networks"></a><span id="Prohibit_roaming_on_mobile_broadband_networks"></span><span id="prohibit_roaming_on_mobile_broadband_networks"></span><span id="PROHIBIT_ROAMING_ON_MOBILE_BROADBAND_NETWORKS"></span>モバイルブロードバンドネットワークでのローミングを禁止する

このポリシーは、Windows がローミング状態にあるモバイルブロードバンドネットワークに接続できないようにします。 既定では、このポリシーは無効になっており、ユーザーは、ローミング中、またはこのようなネットワークへの自動接続を有効にするために、モバイルブロードバンドネットワークに手動で接続することを選択できます。 このポリシーが有効になっていると、ユーザーは接続マネージャーからローミングモバイルブロードバンドネットワークを選択できません。

## <a name="span-idnetwork_preferencesspanspan-idnetwork_preferencesspanspan-idnetwork_preferencesspannetwork-preferences"></a><span id="Network_preferences"></span><span id="network_preferences"></span><span id="NETWORK_PREFERENCES"></span>ネットワークの基本設定


どのような接続を維持するかを検討する場合、Windows はいくつかの特徴を使用して、優先するネットワークを決定します。 これは、ルーティングではなく、特定のインターフェイスへの接続を維持するかどうかを決定する場合にのみ使用されます。 接続されたインターフェイスが論理的に切断されていない場合、ルーティングはルーティングテーブルのメトリックによって決定されます。 ルートメトリックが手動で指定されていない場合、Windows はアダプターのリンク速度に基づいてルートメトリックを自動的に割り当てます。

### <a name="span-idconnection_prioritiesspanspan-idconnection_prioritiesspanspan-idconnection_prioritiesspanconnection-priorities"></a><span id="Connection_priorities"></span><span id="connection_priorities"></span><span id="CONNECTION_PRIORITIES"></span>接続の優先順位

Windows は、次の順序で接続の優先順位を付けます。

1.  イーサネット ネットワーク

2.  現在のユーザーセッション中に手動で接続されたネットワーク

3.  インターネットと、PC が参加している Active Directory ドメインの両方に接続するネットワーク

4.  現在接続されている Wi-fi ネットワークのシグナルの強さ

5.  PC の優先ネットワークリスト

リンク速度は、現在接続されているインターフェイス間のルーティング動作に影響しますが、ネットワークのリンク速度やスループットに基づいて、接続の決定が行われることはありません。 モバイルブロードバンドネットワークと Wi-fi ネットワークの間の接続設定をモバイルブロードバンドネットワークの現在の速度に基づいて変更するように Windows を構成することはできません。 両方が接続されている場合、ユーザーまたはデスクトップアプリはルートメトリックを変更して、ルーティングの設定に影響を与えることができます。

### <a name="span-idsignal_strengthspanspan-idsignal_strengthspanspan-idsignal_strengthspansignal-strength"></a><span id="Signal_strength"></span><span id="signal_strength"></span><span id="SIGNAL_STRENGTH"></span>シグナルの強さ

Windows 8 および Windows 8.1 の場合、現在接続されている Wi-fi ネットワークの信号の強度が非常に低いことを Windows が検出した場合、ネットワーク接続の中断を避けるために、モバイルブロードバンドネットワーク (ポリシーによって許可されている場合) を接続することを選択できます。 これにより、ユーザーがワイヤレスアクセスポイントから移動するときの移行をスムーズに行うことができます。

信号の強さが接続を維持できなくなるまで、より優先される Wi-fi ネットワークが切断されることはありません。 シグナルの強さが向上すると、Windows はモバイルブロードバンドアダプターをソフト切断する場合があります。

Windows 10 では、Wi-fi 信号強度は使用されません。

### <a name="span-idpreferred_network_listspanspan-idpreferred_network_listspanspan-idpreferred_network_listspanpreferred-network-list"></a><span id="Preferred_network_list"></span><span id="preferred_network_list"></span><span id="PREFERRED_NETWORK_LIST"></span>優先するネットワークの一覧

ほとんどの場合、優先ネットワークの一覧によって、Windows が接続に使用するワイヤレスネットワークプロファイルが決まります。 Windows 8 より前の場合、この一覧は Wi-fi ネットワークにのみ適用されます。 Windows 8、Windows 8.1、Windows 10 では、モバイルブロードバンドネットワークを含めることもできます。

### <a name="span-idautomatic_generationspanspan-idautomatic_generationspanspan-idautomatic_generationspanautomatic-generation"></a><span id="Automatic_generation"></span><span id="automatic_generation"></span><span id="AUTOMATIC_GENERATION"></span>自動生成

Windows 8、Windows 8.1、および Windows 10 では、ユーザーの操作に基づいて優先ネットワークの一覧が自動的に更新されます。 手動接続または切断を行うと、今後同じ動作が自動的に行われるように、ネットワークの一覧が更新されます。

次のユーザー操作によって、優先ネットワークの一覧が変更されます。

-   **最初にネットワークに接続し**ています新しいネットワークがネットワークの一覧に追加されます。 ユーザーは、今後ネットワークを自動的に接続するかどうかを指定します。

    -   新しい Wi-fi ネットワークに初めて接続すると、ネットワークが最も優先度の高いネットワークになります。

    -   新しいモバイルブロードバンドネットワークに初めて接続すると、ネットワークが最も優先度の低いネットワークになります。

-   **Wi-fi ネットワークに手動で接続する**一覧の上位にあるその他の Wi-fi ネットワークは、一覧に新しく接続されたネットワークの下に移動されます。 ユーザーは、今後ネットワークを自動的に接続するかどうかを指定します。

-   **ネットワークからの切断**Windows は今後、このネットワークに自動的に接続することはありません。 ユーザーが今後この設定を変更した場合、ネットワークの一覧に残ります。

### <a name="span-idgroup_policyspanspan-idgroup_policyspanspan-idgroup_policyspangroup-policy"></a><span id="Group_Policy"></span><span id="group_policy"></span><span id="GROUP_POLICY"></span>グループ ポリシー

グループポリシーによって作成された wi-fi プロファイルは、ネットワークの一覧の一番上にあります。 ユーザーは、手動でこれらのネットワークから切断することも、他のネットワークに手動で接続することもできます。ただし、これらのネットワークはグループポリシーによって削除されるまで、ネットワークの一覧の一番上の位置にとどまります。

### <a name="span-idcarrier-provisioning_metadataspanspan-idcarrier-provisioning_metadataspanspan-idcarrier-provisioning_metadataspancarrier-provisioning-metadata"></a><span id="Carrier-provisioning_metadata"></span><span id="carrier-provisioning_metadata"></span><span id="CARRIER-PROVISIONING_METADATA"></span>キャリア-プロビジョニングメタデータ

モバイルブロードバンドおよび Wi-fi ホットスポットオペレーターは、[**プロビジョニングエージェント**](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent)または[**msProvisionNetworks**](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85)) api を使用して、Windows に一連のモバイルブロードバンドおよび wi-fi プロファイルを提供します。

最初にプロビジョニングされたオペレーターが作成したプロファイルは、既存のネットワークリストの上部 (Wi-fi のみ) または下部 (モバイルブロードバンドが含まれている場合) に追加されます。 ネットワークの一覧でユーザーがプロビジョニングするネットワークの位置には影響を与えることはできません。 ただし、ネットワークの一覧でネットワークの相対順序を定義できます。

ユーザーの操作によって、プロビジョニングメタデータのアプリケーション間でネットワークの一覧が変更される場合があります。 プロビジョニングメタデータを再適用すると、目的のネットワークの順序が復元されます。 ただし、並べ替えられたネットワークのセットは、ユーザーがネットワークを移動した最も低い位置に移動されます。

プロビジョニングメタデータ内のネットワークの設定は、次のように決定されます。

1.  各ネットワークプロファイルのオプションの priority 属性

2.  メディアの種類 (Wi-fi はモバイルブロードバンドより優先されます)

3.  XML ファイルに指定されている順序

### <a name="span-idmanual_modificationspanspan-idmanual_modificationspanspan-idmanual_modificationspanmanual-modification"></a><span id="Manual_modification"></span><span id="manual_modification"></span><span id="MANUAL_MODIFICATION"></span>手動による変更

Windows 8 より前の場合、Wi-fi 優先ネットワークの一覧は、コントロールパネルの [ワイヤレスネットワークの管理] でユーザーにアクセスできました。 テレメトリは、この機能にアクセスしたユーザーがほとんどいないことを示します。 また、このユーザーインターフェイスは wi-fi のみに関連付けられており、Wi-fi とモバイルブロードバンドの間に設定を組み込むことができませんでした。

ほとんどのユーザーは、ネットワークの一覧を手動で変更する必要はありません。 ただし、特定のユーザーまたはアプリケーションでは、そのために必要な場合があります。

### <a name="span-iduser_interfacespanspan-iduser_interfacespanspan-iduser_interfacespanuser-interface"></a><span id="User_interface"></span><span id="user_interface"></span><span id="USER_INTERFACE"></span>ユーザーインターフェイス

範囲内にあるときに、優先するネットワークの一覧からプロファイルを削除するには、ネットワークを右クリックし、[**このネットワークを忘れる**] を選択します。 範囲内にないネットワークは、ユーザーインターフェイスを使用して一覧から削除することはできません。

### <a name="span-idwin32_apisspanspan-idwin32_apisspanspan-idwin32_apisspanwin32-apis"></a><span id="Win32_APIs"></span><span id="win32_apis"></span><span id="WIN32_APIS"></span>Win32 Api

アプリケーションでは、適切なメディア固有の API を使用して、ネットワークの一覧に新しいプロファイルを作成できます。

-   Wi-fi ネットワークの場合は、 [**WlanSetProfile**](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlansetprofile)関数を使用します。

-   モバイルブロードバンドネットワークの場合は、 [**Imbnconnectionprofilemanager:: CreateConnectionProfile**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionprofilemanager-createconnectionprofile)メソッドを使用します。

ネットワークの一覧の順序を変更するには、 [**WcmSetProfileList**](https://docs.microsoft.com/windows/desktop/api/wcmapi/nf-wcmapi-wcmsetprofilelist)関数を使用します。 [**WlanSetProfileList**](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlansetprofilelist)関数を使用しないことをお勧めします。これは、ネットワークリスト内のモバイルブロードバンドプロファイルが意図せずに行われる可能性があるためです。

ネットワークの一覧からプロファイルを削除するには、適切なメディア固有の API を使用します。

-   Wi-fi ネットワークの場合は、 [**WlanDeleteProfile**](https://docs.microsoft.com/windows/desktop/api/wlanapi/nf-wlanapi-wlandeleteprofile)関数を使用します。

-   モバイルブロードバンドネットワークの場合は、 [**Imbnconnectionprofile::D e)**](https://docs.microsoft.com/windows/desktop/api/mbnapi/nf-mbnapi-imbnconnectionprofile-delete)メソッドを使用します。

### <a name="span-idcommand-linespanspan-idcommand-linespanspan-idcommand-linespancommand-line"></a><span id="Command-line"></span><span id="command-line"></span><span id="COMMAND-LINE"></span>コマンドライン

ユーザーまたはスクリプトは、適切なメディア固有のコマンドを使用して、ネットワークの一覧に新しいプロファイルを作成できます。

-   Wi-fi ネットワークの場合は、 **netsh wlan**の [プロファイルの追加] コマンドを使用します。

-   モバイルブロードバンドネットワークの場合は、 **netsh mbn**の [プロファイルの追加] コマンドを使用します。

ネットワークの一覧にある Wi-fi プロファイルの順序は、 **netsh wlan set profileorder**コマンドを使用して変更できます。 ただし、この方法は推奨されていないため、一覧にあるモバイルブロードバンドプロファイルの位置を意図しない方法で妨害することができます。

ネットワークの一覧からプロファイルを削除するには、適切なメディア固有のコマンドを使用します。

-   Wi-fi ネットワークの場合は、 **netsh wlan**の [プロファイルの削除] コマンドを使用します。

-   モバイルブロードバンドネットワークの場合は、 **netsh mbn delete profile**コマンドを使用します。

### <a name="span-idconflict_resolutionspanspan-idconflict_resolutionspanspan-idconflict_resolutionspanconflict-resolution"></a><span id="Conflict_resolution"></span><span id="conflict_resolution"></span><span id="CONFLICT_RESOLUTION"></span>競合の解決

同じネットワークに複数のプロファイルが存在する場合、Windows 8 と Windows 8.1 は、次のロジックを使用して、使用するプロファイルを決定します。

1.  **プロファイルの種類**

    1.  グループポリシープロファイルは、ユーザーが作成したプロファイルより優先されます。

    2.  すべてのユーザープロファイルは、単一ユーザープロファイルより優先されます。

2.  **インターフェイスの到着**最後にインストールされたインターフェイスのプロファイルが使用されます。

 

 





