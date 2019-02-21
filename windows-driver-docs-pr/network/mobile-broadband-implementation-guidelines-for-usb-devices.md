---
title: USB デバイスのモバイル ブロード バンド実装ガイドライン
description: このトピックでは、モバイル ブロード バンド デバイス製造元が準拠している USB デバイスを Windows の生成に役立つ具体的な実装ガイダンスを提供します。
ms.assetid: 1E8CBBCC-9E35-49AA-85A7-DFAD6772B164
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4fb0abb5cbfcf18ab80041096989d0b2532cbdf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536687"
---
# <a name="mobile-broadband-implementation-guidelines-for-usb-devices"></a>USB デバイスのモバイル ブロード バンド実装ガイドライン


このトピックでは、モバイル ブロード バンド デバイス製造元が準拠している USB デバイスを Windows の生成に役立つ具体的な実装ガイダンスを提供します。 組み合わせて使用する必要がありますが、 [USB NCM モバイル ブロード バンド インターフェイス モデル (MBIM) V1.0 仕様](https://usb.org/document-library/mobile-broadband-interface-model-v10-errata-1-and-adopters-agreement)リリース-IF Device Working Group です。

このトピックの情報に適用されます。

-   Windows 8
-   Windows 8.1

## <a name="delaying-mbim-open"></a>Mbim を遅らせる


MBIM デバイスは、ホストから MBIM 開いているメッセージを受け取ったときに初期化を完了に時間を必要があります。 デバイスがその初期化が開いている MBIM メッセージに応答する前に完了するまで待ちます。 MBIM などのエラー ステータス メッセージ、デバイスが応答する必要がありますいない\_状態\_ビジー MBIM 開いてメッセージを使用したデバイスをポーリングするホストのことを期待します。 MBIM 以外の状態で MBIM 開くを応答\_状態\_成功した場合、ホスト上の初期化プロセスを終了します。

## <a name="multi-carriermulti-subscription"></a>マルチ キャリア\\マルチ サブスクリプション


参照してください**実装マルチモードおよびマルチ対応 MB デバイスの IHV ガイダンス**詳細についてはします。

**MBIM\_CID\_ホーム\_プロバイダー**

MBIM デバイスは設定 MBIM に失敗することはない\_CID\_ホーム\_に説明した状況では、次の一覧表示されている状態コードで要求をプロバイダー。 次の状態に対して有効ではクエリ MBIM\_CID\_ホーム\_プロバイダーの要求はセットの要求には適用されません。

-   **MBIM\_状態\_SIM\_いない\_INSERTED** -MBIM デバイスは設定 MBIM に失敗することはない\_CID\_ホーム\_MBIMとして状態プロバイダー要求\_状態\_SIM\_いない\_新しいホーム プロバイダー SIM はあるが、古いホーム プロバイダー SIM が挿入されていない場合に挿入します。
-   **MBIM\_状態\_不良\_SIM** -MBIM デバイスは MBIM の設定に失敗することはありません\_CID\_ホーム\_MBIM で要求をプロバイダー\_状態\_が正しくありません\_SIM、SIM 新しいホーム プロバイダーをお勧めが古いホーム プロバイダー SIM が不良ではない場合。
-   **MBIM\_状態\_PIN\_REQUIRED** -MBIM デバイスは MBIM の設定に失敗することはありません\_CID\_ホーム\_MBIM で要求をプロバイダー\_状態\_PIN\_古いまたは新しい SIM がロックされている pin であるかに関係なく必要です。

**MBIM\_CID\_VISIBLE\_プロバイダー**

-   **MBIM\_状態\_SIM\_いない\_INSERTED** -とき MBIM\_VISIBLE\_プロバイダー\_MBIMVisibleProvidersActionRestrictedScan にアクションが設定されています。MBIM デバイスは MBIM に失敗することはありません\_CID\_VISIBLE\_MBIM で要求をプロバイダー\_状態\_SIM\_いない\_ために、挿入の SIM、現在のホーム プロバイダーは存在しません。
-   **MBIM\_状態\_PIN\_REQUIRED** -とき MBIM\_VISIBLE\_プロバイダー\_MBIM デバイスは許可されません MBIMVisibleProvidersActionRestrictedScan にアクションが設定されています。MBIM 失敗\_CID\_VISIBLE\_MBIM で要求をプロバイダー\_状態\_PIN\_現在ホーム プロバイダー SIM がロックされている PIN のために必要な。

## <a name="responding-to-pin-operations"></a>ピン操作に対する応答


MBIM デバイスに対応するときにこれらのガイドラインに従う必要があります**MBIMPinOperationEnter**要求。

-   成功した**MBIMPinOperationEnter**デバイスが不要になった、PIN を必要とする場合は、要求、デバイスの必要がありますの状態に設定 MBIM\_状態\_成功と**MBIM\_暗証番号(pin)\_INFO::Pin 型**に**MBIMPinTypeNone します。**
-   デバイスは、MBIM に状態を設定する必要があります\_状態\_PIN が要求された状態で既にときに、暗証番号 (pin) を有効にし、ピン留めすると無効化の操作の成功します。 デバイスを設定する必要があります**MBIM\_PIN\_INFO::PinType**に**MBIMPinTypeNone**します。 他のメンバーは無視されます。
-   [有効] に無効になっているから PIN モードが変更されると、暗証番号 (pin) 状態であるか**MBIMPinStateUnlocked**します。
-   PIN1 が有効になっている場合、暗証番号 (pin) の状態は次のようになります。 **MBIMPinStateLocked**電源を入れ、デバイスの場合。
-   他のすべてのピンの状態の固定がから変更できます**MBIMPinStateUnlocked**に**MBIMPinStateLocked**モバイル ブロード バンド デバイスの特定の条件によって異なります。
-   PIN がサポートされていません。デバイスが MBIM に状態を設定する必要がある場合は、デバイスでは、暗証番号 (pin) の操作はサポートされていない、\_状態\_いいえ\_デバイス\_サポートします。 たとえばを有効にして、暗証番号 2 を無効化は通常サポートされませんモバイル ブロード バンド デバイスで上記のエラー コードを返す必要があるため。 その他のすべてのメンバーは無視されます。
-   PIN を入力する必要があります。デバイスが MBIM に状態を設定する必要があります暗証番号 (pin) の操作では、PIN を入力する必要がある場合\_状態\_PIN\_REQUIRED と**MBIM\_PIN\_INFO::PinType** に**MBIMPinTypeXxx**します。 他のメンバーは無視されます。
-   PIN の変更操作:MBIM で無効な状態を変更する要求を返す必要がある場合は、デバイスが有効になっている状態にある場合にのみ、暗証番号 (pin) の値の変更を制限、\_状態\_PIN\_無効になっています。
-   PIN Retrial:失敗した場合、デバイスは、MBIM に状態を設定する必要があります\_状態\_エラー、および**MBIM\_PIN\_INFO::PinType**で指定されているのと同じ値に**MBIM\_設定\_PIN**します。 以外の他のメンバーは無視されます**MBIM\_PIN\_INFO::RemainingAttempts**します。 これは、正しくない PIN を入力するときに発生します。
-   ブロックをピン留めします。PIN がブロックされているときに数**MBIM\_PIN\_INFO::RemainingAttempts**は 0 です。 操作は使用できません、暗証番号 (pin) のブロックを解除する場合は、デバイスは、MBIM に状態を設定する必要があります\_状態\_障害と**MBIM\_PIN\_INFO::PinType**に**MBIMPinTypeNone**. **MBIM\_PIN\_INFO::RemainingAttempts**を 0 に設定する必要があり、その他のすべてのメンバーは無視されます。
    **注**  操作のブロックを解除、デバイスは、暗証番号 (pin) をサポートしている場合は、デバイスは、要求に応答する PIN ブロック解除の手順を実行する必要があります。

     

-   暗証番号のブロック解除:PIN がブロックされているときに**MBIM\_PIN\_INFO::RemainingAttempts**は 0 です。 暗証番号のブロックを解除するには、該当する場合、デバイスは、対応する PUK を要求する可能性があります。 この場合、デバイスは、MBIM の状態を設定する必要があります\_状態\_障害、 **MBIM\_PIN\_INFO::PinType** 、対応する**MBIMPinTypeXxxPUK**、 **PinState**に**MBIMPinStateLocked**、および**MBIM\_PIN\_INFO::RemainingAttempts**数である必要があります試行の有効な PUK を入力できます。
-   デバイスまたは SIM で結果をブロックに暗証番号 (pin) がブロックされた場合、デバイスは、MBIM を送信する必要が\_CID\_サブスクライバー\_準備\_状態通知を**ReadyState** に設定**MBIMSubscriberReadyStateDeviceLocked します。**
-   PIN1 ブロック時にアクティブな PDP コンテキストがある場合、デバイスする必要があります PDP コンテキストを非アクティブ化し、PDP 非アクティブ化に関するオペレーティング システムに通知を送信されて、状態の変更をリンクします。
-   成功した要求の場合、デバイスは、MBIM に状態を設定する必要があります\_状態\_成功します。 他のメンバーは無視されます。
-   失敗しました**MBIMPinOperationEnter**要求すると、デバイスは、MBIM に状態を設定する必要があります\_状態\_失敗し、次の詳細に従って該当するデータを含めます。
    -   PIN を無効になっているまたは PIN が予期されていません。デバイスを設定する必要があります MBIMPinOperationEnter セットは、対応するピンが無効か、または現在ないデバイスが予期されるときに、要求、 **MBIM\_PIN\_INFO::PinType**に**MBIMPinTypeNone**します。 その他のすべてのメンバーは無視されます。
    -   PIN がサポートされていません。デバイスが MBIM に状態を設定する必要がある場合は、デバイスでは、特定の暗証番号 (pin) はサポートされていない、\_状態\_いいえ\_デバイス\_サポートします。
    -   PIN Retrial:このモードでデバイスには、PIN として再入力する、 **MBIM\_PIN\_INFO::RemainingAttempts**値がまだゼロ以外の暗証番号 (pin) のこの特定の型。 デバイスを設定する必要があります**MBIM\_PIN\_INFO::PinType**のと同じ値に**MBIM\_PIN\_INFO::PinType**で**MBIM\_設定\_PIN**します。
    -   ブロックをピン留めします。PIN がブロックされているときに**MBIM\_PIN\_INFO::RemainingAttempts**は 0 です。 操作は使用できません、暗証番号 (pin) のブロックを解除する場合は、デバイスは、MBIM に状態を設定する必要があります\_状態\_障害と**MBIM\_PIN\_INFO::PinType**に**MBIMPinTypeNone**. その他のすべてのメンバーは無視されます。
        **注**  操作のブロックを解除、デバイスは、暗証番号 (pin) をサポートしている場合は、デバイスは、要求に応答する PIN ブロック解除の手順を実行する必要があります。

         

    -   PIN のブロックを解除します。PIN がブロックされているときに**MBIM\_PIN\_INFO::RemainingAttempts**は 0 です。 PIN のブロックを解除するには、該当する場合、デバイスは、対応するピンのロックを解除キー (PUK) を要求する可能性があります。 この場合、デバイスを設定する必要があります**MBIM\_PIN\_INFO::PinType** 、対応する**MBIMPinTypeXxxPUK**に関連する詳細。
    -   PUK を禁止します。失敗した試行の回数が入力するための事前定義された値を超えたかどうか、 **MBIMPinTypeXxxPUK**、PUK がブロックされました。 MBIM に状態を設定してこのデバイスで通知する必要があります\_状態\_障害と**MBIM\_PIN\_INFO::PinType**に**MBIMPinTypeNone**します。 デバイスが、MBIM を送信する必要があります PUK1 がブロックされている場合に\_CID\_サブスクライバー\_準備ができて\_で状態を**ReadyState**に設定**MBIMSubscriberReadyStateBadSim**.
    -   MBIM デバイスに対応するときにこれらのガイドラインに従う必要があります**MBIMPinOperationEnable**、 **MBIMPinOperationDisable**、または**MBIMPinOperationChange**要求。

## <a name="auto-packet-service-attach"></a>自動パケット サービス接続します。


自動パケット サービス接続をサポートする MBIM デバイスは、それぞれの判断でのモバイル、ネットワークからのパケットのサービスの取り外しと添付ファイルを管理します。 ホストは、ユーザーの要求にこのようなデバイスにアタッチ要求を送らないことがあります。 ときに、デバイスは次のように処理するホストからアタッチ要求を受け取ります。

-   • デバイスが接続されており、アタッチ操作の途中ではなく、し、それにアタッチできる場合は、モバイル ネットワークでの新しいアタッチ手順を開始する必要があります。
-   • デバイスが接続されていない場合、自動アタッチの途中で操作しがの自動アタッチ操作が完了し、自動アタッチ操作の状態を持つホストからアタッチ要求の完了を待機する必要があります。
-   • ホストからアタッチ要求を正常に完了する必要がありますが、デバイスが既にアタッチされている場合。

## <a name="signal-strength-loss-and-data-connection-loss"></a>信号強度の損失とデータ接続が失われる


デバイスが失ったときに信号強度、デバイスを示す必要があります**MBIMActivationStateDeactivated**続けて**MBIMPacketServiceStateDetached**続けて**MBIMRegisterStateDeregistered**をこの順序で。 パケット サービスがデバイスでアクティブ化されるコンテキストを示す必要があります、デバイスが紛失した場合は**MBIMActivationStateDeactivated**続けて**MBIMPacketServiceStateDetached**をこの順序で。 次のシーケンス図は、ホストとデバイス間の相互作用を示しています。

![シーケンス図は、ホストとデバイス間の相互作用を示しています。](images/mbimplementationguidelinesusb.png)

## <a name="dns-server-information"></a>DNS サーバー情報


MBIM 経由で (MBIM 10.5.20.1 セクションで定義) された基本的な IP 情報が入力されたら\_CID\_IP\_構成では、DNS サーバーの情報 (MBIM 10.5.20.1 セクションで定義) されたことができます提供することも MBIM を介して\_CID\_IP\_構成します。 DNS サーバーの情報が更新されると、MBIM\_CID\_IP\_構成には、前に取得の完全な IP の基本的な情報が必要です。 MBIM を使って DNS サーバーの情報を提供できます\_CID\_IP\_MBIM を使用して基本的な IP 情報が指定されていない場合でも構成\_CID\_IP\_構成します。 これは、IPv4 と IPv6 の両方に適用されます。

## <a name="ipv6"></a>IPv6


(MBIM 10.5.20.1 セクションで定義) として基本 IP 情報、期待される IP 層の構成メカニズムはルーター アドバタイズ (RA) です。 (MBIM 10.5.20.1 セクションで定義) と DNS サーバーは、予想される IP 層の構成メカニズムは DHCPv6 です。

-   **RA の基本 IP 情報**MBIM デバイスは、RA パケットをホストに転送されるとする必要がありますいない RA パケットを傍受または基本的な IP を提供を許可する必要があり、モバイル ネットワークで RA を使用して基本的な IP 情報 (MBIM 10.5.20.1 セクションで定義) されたを提供する場合 -MBIM 経由の RA パケットに含まれている情報\_CID\_IP\_構成します。
-   **RA から DNS サーバー情報**-唯一 IP 層の構成のメカニズム (MBIM 10.5.20.1 セクションで定義) された DNS サーバーの情報の Windows でサポートされているは DHCPv6 します。 MBIM デバイスは、DNS サーバーの情報を構成する必要があります MBIM 経由の RA で存在する場合でも\_CID\_IP\_構成します。
-   **IP の基本的な情報と DHCPv6 の DNS サーバー情報**- 場合は、モバイル ネットワークでは基本的な IP および DNS サーバーについて (MBIM 10.5.20.1 セクションで定義) された DHCPv6 から MBIM デバイスは、DHCPv6 のパケットを転送するを許可する必要がありますし、ホストにする必要がありますいない DHCPv6 パケットを傍受や IP の基本的な情報と MBIM 経由で DHCPv6 パケットに存在する DNS サーバーの情報を提供\_CID\_IP\_構成します。

## <a name="mbimcidradiostate"></a>MBIM\_CID\_ラジオ\_状態


MBIM デバイスは MBIM に失敗することはありません\_CID\_ラジオ\_MBIM の状態が状態操作\_状態\_SIM\_いない\_SIM が存在しない場合に挿入します。 ラジオ操作は、SIM 休暇のためできませんでしたいない必要があります。

## <a name="byte-ordering-requirements-for-authentication-cids"></a>認証 Cid のバイト オーダー要件


以下のバイト配列フィールド内のデータは、ホストのバイト順でなければなりません。

**MBIM\_CID\_SIM\_認証**

MBIM\_SIM\_AUTH\_要求数

1.  Rand1
2.  Rand2
3.  Rand3

**MBIM\_CID\_AKA\_認証**

MBIM\_AKA\_AUTH\_要求数

1.  rand 関数
2.  Autn

MBIM\_AKA\_AUTH\_情報

1.  res
2.  IK
3.  CK
4.  Auts

**MBIM\_CID\_AKAP\_認証**

MBIM\_AKAP\_AUTH\_要求数

1.  rand 関数
2.  Autn

MBIM\_AKAP\_AUTH\_情報

1.  res
2.  IK
3.  CK
4.  Auts

## <a name="setting-link-mtu"></a>リンク MTU の設定


Windows では、デバイスの初期化中にのみリンクの最大転送単位 (MTU) の構成をサポートします。 Windows では、MBIM を使用して報告 MTU に基づいてリンク MTU は更新されません\_CID\_IP\_構成します。 デバイスはサポートされているネットワーク リンク MTU、MBIM を使用して通信する必要があります\_機能\_DESCRIPTOR.wMaxSegmentSize します。 リンク MTU の値がこの方法で報告は、少なくとも 1280 から最大 1500 台必要があります。

 

 





