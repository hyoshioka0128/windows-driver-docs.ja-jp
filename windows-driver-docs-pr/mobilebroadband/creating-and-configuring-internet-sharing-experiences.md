---
title: 作成とインターネットの共有エクスペリエンスの構成
description: 作成とインターネットの共有エクスペリエンスの構成
ms.assetid: 11906ee4-68f5-4be6-a3ab-6af3253c8a11
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02012ea3e6f7b39908a02d6a35df8adc099c3c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552847"
---
# <a name="creating-and-configuring-internet-sharing-experiences"></a>作成とインターネットの共有エクスペリエンスの構成


インターネット共有をテザリングとも呼ばが 1 つまたは複数の他のいないデバイスをモバイルでのモバイル ブロード バンド ネットワーク接続を共有するユーザーを有効にする Windows 8.1 で追加されましたブロード バンド対応します。 Bluetooth、USB ケーブルの従来のメカニズムが含まれます。 ただし、Wi-fi できます提供、高速、簡単にモバイル ブロード バンド接続構成はほとんど必要があるために、個人用のホット スポット、モバイル ホット スポットなどのメカニズムを共有により、高速データ転送、および使い慣れた Wi-fi に依存しています接続するプロセス。

Windows 8.1 および Windows 10 をオンにし、標準の Wi-fi ネットワークが場合と同様に、ケーブルのアクセス ポイントと呼ばれるインターネット共有を構成している Pc に接続することでさらに機能の共有をインターネットに拡張します。

## <a name="span-idturnoninternetsharingspanspan-idturnoninternetsharingspanspan-idturnoninternetsharingspanturn-on-internet-sharing"></a><span id="Turn_on_Internet_Sharing"></span><span id="turn_on_internet_sharing"></span><span id="TURN_ON_INTERNET_SHARING"></span>インターネット共有を有効に


インターネット共有可能にモバイル ブロード バンド対応のデバイスで、設定チャームを使用しています。 インターネット共有をオンにすると、Wi-fi ネットワークに接続できる任意のデバイスに接続できます。

**インターネット共有を有効にするには**

1.  **設定**チャームをクリックします**PC 設定の変更**、 をクリックし、**ネットワーク**します。

2.  で、**モバイル ブロード バンド**見出しで、ネットワーク名をクリックします。

3.  **モバイル ブロード バンド** ページで、ネットワークのインターネット共有を有効にします。 モバイル ブロード バンド ネットワークが切断された場合、デバイスはモバイル ブロード バンド ネットワークに Wi-fi ネットワークをセットアップする前に自動的に接続されます。

4.  必要なサービス メタデータ パッケージを作成する場合、PC は、権利チェックを実行する Microsoft Store モバイル ブロード バンドのアプリを示すイベントをトリガーします。 PC、モバイル ブロード バンド アプリ インターネット共有を有効にする前に応答するまで待機します。 サービス メタデータ パッケージの作成の詳細については、次を参照してください。[サービス メタデータを作成するための開発者ガイド](developer-guide-for-creating-service-metadata.md)します。

5.  モバイル ブロード バンド ネットワークが有効にすると、必要な権利チェックに合格した、カスタマイズされたネットワークの名前を持つ Wi-Fi Direct 自律的なグループの所有者のモードを使用するプライベートの Wi-fi ネットワークを使用して、モバイル ブロード バンド接続が共有されます。 これにより、任意のデバイスの Wi-fi をネットワークに接続できること。

    **注**  モバイル ブロード バンド ネットワークのアイコンは、ネットワークを他のユーザーによって共有されていることに注意してください。 お客様を支援する Windows 全体で自動的に更新されます。

     

6.  インターネットの共有を有効にしたらから、**モバイル ブロード バンド**] ページで [**編集**ネットワーク名とパスワードを変更します。

    -   Wi-fi ネットワークには、WPA2 PSK を使用する必要があります。

    -   ネットワーク名は、既定値に設定*&lt;デバイス名&gt; &lt;4 桁の数字&gt;* します。 既定のネットワーク名は、ネットワークの一覧に合わせて完全な短いと複数のデバイスを区別するのに十分な一意の中で名前がユーザーにわかりやすいものであることを確認に最適化されます。

    -   パスワードは、既定値は 12 のランダムな数値に設定されます。

    -   パスワードは、少なくとも 8 文字の長さである必要があります。

    -   Wi-fi ネットワークがネットワーク名またはパスワードが変更されたときに再起動されます。

インターネットの共有がオンにすると、次の処理が行われます。

-   クライアント デバイス上のネットワークは、モバイル ブロード バンド ネットワーク上の不要な帯域幅の消費量を減らす従量制課金接続として自動的に設定されます。 これは、ネットワーク コストを定義する、Wi-fi ビーコン/プローブ応答フレームで、Windows 8 のベンダー固有の情報要素を使用して行います。 Windows 8.1 では、Wi-fi ビーコン/プローブ応答フレーム内の要素が追加されたを別のベンダー固有の情報は、ネットワークがケーブルのネットワークである場合に、クライアント デバイスを通知します。 この追加は、Windows 8.1 および Windows 10 の両方に影響します。

-   インターネットの共有がオンにすると、PC がクライアント デバイスには、インターネット接続が失われないことを確認するには、コネクト スタンバイやスリープに移動できません。

-   データの量は、モバイル ブロード バンドのアプリを使用してクライアント デバイスで使用されているを確認できます。

-   最後のクライアント デバイスがテザリングされたネットワークから切断された後にインターネット共有を 5 分間待機します。 その他のクライアント デバイスが接続できない場合は、インターネットの共有が無効になり、PC が通常の電源状態に戻ります。

-   エンタープライズ管理者としては、インターネット共有を無効にグループ ポリシーを使用しています。

## <a name="span-idconnecttoatetherednetworkspanspan-idconnecttoatetherednetworkspanspan-idconnecttoatetherednetworkspanconnect-to-a-tethered-network"></a><span id="Connect_to_a_tethered_network"></span><span id="connect_to_a_tethered_network"></span><span id="CONNECT_TO_A_TETHERED_NETWORK"></span>テザリングされたネットワークに接続します。


同様に、他の Wi-fi ネットワークに接続する Wi-fi デバイスを使用して、テザリングされたネットワークに接続することができます。 ただし、ユーザーは、Windows 8.1 または Windows 10 を実行しているデバイスの両方で同じ Microsoft アカウント資格情報でテザリングされたネットワークに接続する場合、次の処理が行われます。

-   インターネットの共有が有効でない場合、Windows 8.1 または Windows 10 デバイスを接続したときに、2 つのデバイスが Bluetooth 接続を作成し、インターネット共有を有効にします。

-   接続が自動的にテザリングされたネットワークから資格情報を自動的に取得することによって、(ネットワーク名と SSID) を構成します。

**注**   Bluetooth を使用して自分のデバイスをペアリングする場合、ユーザーはケーブル アクセス ポイントに接続もできます。

 

## <a name="span-idconfigureinternetsharingspanspan-idconfigureinternetsharingspanspan-idconfigureinternetsharingspanconfigure-internet-sharing"></a><span id="Configure_Internet_Sharing"></span><span id="configure_internet_sharing"></span><span id="CONFIGURE_INTERNET_SHARING"></span>インターネット共有を構成します。


いくつかモバイル ネットワーク オペレーター (MNOs) またはモバイルの仮想ネットワークの演算子 (MVNOs) がサポートされないインターネットの共有、ネットワーク上またはインターネット共有をセットアップする前に、権利チェックが必要です。 Windows では、Windows デバイスがネットワーク ポリシーに準拠していることを確認するために必要なコントロールを提供します。 

バージョン 1803 より前の Windows 8、Windows 8.1、または Windows 10 には、サービス メタデータ パッケージを作成して構成する必要があります、 [AllowTethering](allowtethering.md)スキーマ内の要素 ([サービス メタデータ パッケージ スキーマ リファレンス](service-metadata-package-schema-reference.md)). サービス メタデータ パッケージの作成に関する詳細については、次を参照してください。[サービス メタデータを作成するための開発者ガイド](developer-guide-for-creating-service-metadata.md)します。 次の 3 つのオプションがあります。

-   すべてのお客様のインターネット共有を許可します。 (既定値指定されていない場合、サービス メタデータ パッケージの)

-   すべてのお客様のインターネット共有をブロックします。

-   権利チェック後にお客様のインターネット共有を許可します。

Windows 10、バージョン 1803 以降で設定する必要があります、 [**ホット スポット**COSA データベースにおける設定](desktop-cosa-apn-database-settings.md#desktop-cosa-only-settings)適切な値。

場合は、権利チェックが必要ないことを決定する追加情報や機能は必要ありません。 権利チェックが必要な場合は、モバイル ブロード バンド UWP アプリの一部であるバック グラウンド通知イベント ハンドラーを指定することもあります。 Windows 10、バージョン 1803 以降のメソッドを使用して、 [TetheringEntitlementCheckTriggerDetails](https://docs.microsoft.com/uwp/api/windows.networking.networkoperators.tetheringentitlementchecktriggerdetails)ケーブルの権利を確認するための Windows 通知イベントを処理するクラス。 以前のバージョンの Windows では、使用、 [ **NetworkOperatorNotificationEventDetails** ](https://msdn.microsoft.com/library/windows/apps/br207377)クラス。 バック グラウンド通知のイベント ハンドラーを作成する方法の詳細については、次を参照してください。 [mobile operator notifications とシステム イベントを有効にする](enabling-mobile-operator-notifications-and-system-events.md)します。

MOs と MVNOs があるさまざまな要件にどのような PDP コンテキストは、インターネットの共有のために使用する必要があります。 既存の Windows が更新[プロビジョニング XML スキーマ](https://msdn.microsoft.com/library/windows/apps/hh868398)正しいインターネット共有 PDP コンテキスト情報を使用してシステムをプロビジョニングできます。 複数の PDP コンテキストの詳細については、次を参照してください。[複数の PDP コンテキストを使用してアプリの開発](developing-apps-using-multiple-pdp-contexts.md)します。

最大値を構成することもできます。 同時に接続されているクライアント デバイスの数は 10 です。 3 から 10 の間を使用してどこにもこの番号を変更できます[アカウント プロビジョニング](account-provisioning.md)します。

ユーザーの実行がそのデータを誤ってしないことを確認するに表示できますデータ使用状況の統計と非共有のトラフィック、顧客にモバイル ブロード バンド アプリを使用して、 [ **GetNetworkUsageAsync**](https://msdn.microsoft.com/library/windows/apps/dn266073)のメソッド、 [ **ConnectionProfile** ](https://msdn.microsoft.com/library/windows/apps/br207249)クラス。

## <a name="span-idcreateacustominternetsharingappspanspan-idcreateacustominternetsharingappspanspan-idcreateacustominternetsharingappspancreate-a-custom-internet-sharing-app"></a><span id="Create_a_custom_Internet_Sharing_app"></span><span id="create_a_custom_internet_sharing_app"></span><span id="CREATE_A_CUSTOM_INTERNET_SHARING_APP"></span>カスタム インターネット共有アプリを作成します。


ほとんどの演算子には、Windows のユーザー インターフェイスはインターネットの共有の最適なエクスペリエンスが提供されます。 ただし、すべてのハードウェアとデバイス間で一貫したエクスペリエンスを作成するためにすることができます、モバイル ブロード バンド アプリまたはモバイル ブロード バンドへのアクセス権限が付与されている他のアプリに、独自のインターネットの共有ユーザー エクスペリエンスを含めるデバイスです。 Windows でのいくつかの新しい Api を提供する、 [ **Windows.Networking.NetworkOperators 名前空間**](https://msdn.microsoft.com/library/windows/apps/br241148)以下を実行するアプリを有効にします。

-   システムがインターネットの共有の対応を確認します

-   オンとオフ、インターネットの共有

-   クエリを実行して、Wi-fi SSID とネットワークの場合はパスフレーズを構成します。

-   権利チェックを実行します。

-   クエリの接続されたデバイス数と許可されている接続されたデバイスの最大数

-   インターネットの共有状態または接続されたデバイス数の変更に関する通知を受信し、対処

 

 





