---
title: モバイル ブロードバンドの概要
description: モバイル ブロードバンドの概要
ms.assetid: 5193927b-7367-468e-8012-c41f6bd743a3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff34b8902d9f2119f9f5ceabfefa8e19266cb586
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357976"
---
# <a name="overview-of-mobile-broadband"></a>モバイル ブロードバンドの概要


Windows 8、Windows 8.1、および Windows 10 モバイル ネットワーク オペレーターの新しい機会を提供しつつ、ユーザーのモバイル ブロード バンド接続を簡略化します。 ユーザーは、効率的で一貫性のある接続フローを利用できます。 Windows 8、Windows 8.1、および Windows 10 開発リソースは、アカウントの管理および付加価値サービスを含む、顧客との対話にフォーカスすることがあるために、従来の接続管理アプリを開発する必要性を低減します。

Windows 8、Windows 8.1、および Windows 10 再考し、既存のモバイル ブロード バンドのエコシステムを合理化する機会を提供します。

-   モバイル ブロード バンド ハードウェアの以前のバージョンでは、カスタムの Windows ドライバーが必要です。 認定済みのモバイル ブロード バンド デバイスでは現在モバイル ブロード バンド クラス ドライバーを使用したカスタム ドライバーをインストールすることがなく一貫したエクスペリエンスがあります。 この合理化可能性があるサポート オーバーヘッドを削減しながら"だけ works"エクスペリエンスをお客様に提供する機会を表示します。

-   管理エクスペリエンスのカスタマイズされた接続は、Windows の機能を複製し、Windows の残りの部分よりもさまざまな UX モデルがあります。 これらの接続マネージャーは、配置して、演算子と、ISV パートナーによって管理する必要があります。

-   カスタム ドライバーおよびカスタムの接続管理ソフトウェアに対して必要ものでは USB ベースのモバイル ブロード バンド デバイスは、ユーザーの PC にそのカスタム ソフトウェアを配信するためにも USB 記憶域機能を実行する必要があります。 多くの場合、このデュアル モードのデバイスの概念には、ストレージ モードと、ユーザーがネットワークに接続できる前に、追加のタスクを追加、モデムのモードの切り替えをユーザーが必要です。

-   一意のサービスを強調表示し、一意が発生することをお客様に機能します。 Windows 8、Windows 8.1、および Windows 10 は、ユーザー接続にフォーカスする機会を提供を強調表示する、一意の付加価値や、アプリを使って UWP モバイル ブロード バンド、以前の通信事業者アプリ。

## <a name="span-idkeyscenariosspanspan-idkeyscenariosspanspan-idkeyscenariosspankey-scenarios"></a><span id="Key_scenarios"></span><span id="key_scenarios"></span><span id="KEY_SCENARIOS"></span>主なシナリオ


このセクションでは、有効にすることもできますが、現在のモバイル ブロード バンド エクスペリエンスの一部である主なシナリオについて説明します。 アプリと対話する必要があります Windows コンポーネントを計画するときは、これらのシナリオは、ビジネス モデルのコンテキスト内の各を検討します。

-   [プランを購入](#plan-purchase)

-   [アクティブなデバイスを接続します。](#connecting-an-active-device)

-   [Operator notifications とシステム イベント](#operator-notifications-and-system-events)

-   [使用状況とプランの正確なデータを提供します。](#providing-accurate-usage-and-plan-data)

-   [インターネット共有](#internet-sharing)

-   [Wi-fi ホット スポット認証](#wi-fi-hotspot-authentication)

-   [アカウント情報をユーザーに表示します。](#displaying-account-information-to-the-user)

-   [その他のデバイスとアプリのシナリオを有効にします。](#enabling-other-devices-and-app-scenarios)

### <a name="plan-purchase"></a>プランを購入

シームレスなプランの購入エクスペリエンス ユーザー接続を購入するが容易になり、サポートまたは小売り店の介入がなくても新規顧客をそのまま使用する演算子を使用します。 2 つの購入プラン オプションがあります。

-   モバイル ブロード バンド アプリとサービスのメタデータが PC に既にインストールされています。 これは、OEM がモバイル ブロード バンド アプリケーションをプリロードして、Windows イメージまたは別のインターネット接続でのサービス メタデータが使用可能な場所のモバイル ブロード バンド ハードウェアが埋め込まれている Pc の発生する可能性があります。

-   モバイル ブロード バンド アプリとサービスのメタデータが、PC にインストールされていません。 これは、ハードウェア ドングルを接続して、代替のインターネット接続が利用できないときに発生する可能性があります。

プランの購入オプションに関係なく SIM または CDMA モバイル ブロード バンド デバイスの状態に基づいて、さまざまなサブ状態があります。 コールド Sim (関連付けられているプランなし)、ウォーム Sim (プランを受け入れるように準備完了) とホット Sim (プランで既にアクティブな) が購入フローを構成する方法に基づいてさまざまなエクスペリエンスを提示する可能性があります。

### <a name="span-idmobilebroadbandappisalreadyinstalledoranalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisalreadyinstalledoranalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisalreadyinstalledoranalternateinternetconnectionisavailablespanmobile-broadband-app-is-already-installed-or-an-alternate-internet-connection-is-available"></a><span id="Mobile_broadband_app_is_already_installed_or_an_alternate_Internet_connection_is_available"></span><span id="mobile_broadband_app_is_already_installed_or_an_alternate_internet_connection_is_available"></span><span id="MOBILE_BROADBAND_APP_IS_ALREADY_INSTALLED_OR_AN_ALTERNATE_INTERNET_CONNECTION_IS_AVAILABLE"></span>モバイル ブロード バンド アプリが既にインストールされているか、代替のインターネット接続があります。

この場合、embedded デバイス、モバイル ブロード バンド アプリ、およびサービスでメタデータがおそらくインストール済み SIM で PC の前に、ユーザーがサービスをアクティブ化を試みます。 別の方法としては、ユーザーがモバイル ブロード バンドのアプリをまだはありませんが、代替のインターネット接続がアプリをダウンロードします。 次の手順は、SIM が挿入されると自動的に発生します。

1.  モバイル ブロード バンド サービスは、International Mobile IMSI (Subscriber Identity)、GSM ネットワーク、CDMA ネットワークでは、プロバイダー ID (SID) または CDMA ネットワークのプロバイダー名 Integrated 回線カード ID (ICCID) 読み取りし、ハードウェア Id (のセットを生成しますHWIDs)。

    **注**  この手順は、OEM がない SIM の挿入し、モバイル ブロード バンドのアプリとサービスのメタデータを事前に読み込まれた場合にのみ必要です。

     

2.  PC がインターネットに接続されているときに、HWIDs は Windows メタデータとインターネット サービス (WMIS) に送信されます。 WMIS では、演算子を識別し、適切なサービス メタデータ パッケージを返します。

    **注**  この手順は、OEM がない SIM の挿入し、モバイル ブロード バンドのアプリとサービスのメタデータを事前に読み込まれた場合にのみ必要です。

     

3.  Windows では、サービス メタデータを使用して識別し、モバイル ブロード バンドのアプリを Microsoft Store から取得します。 アプリが自動的にインストールされます。 Windows 8.1 および Windows 10 では、スタート画面に、アプリはピン留めされていません。

    **注**  この手順は、OEM がない SIM の挿入し、モバイル ブロード バンドのアプリとサービスのメタデータを事前に読み込まれた場合にのみ必要です。

     

4.  Windows 接続マネージャーでネットワークの一覧で、演算子のロゴや名前が表示されます。 ユーザーは、ネットワークに接続できます。

5.  Windows 接続マネージャーは、ネットワーク プロファイルの構成情報をサービス メタデータを使用して接続しようとします。 次の手順は、接続の結果によって異なります。

    -   最初の接続が成功すると、インターネット接続が利用できる場合は、さらに何も起こりません。 ユーザーは、サービスを購入したが、アクティブなアカウントを持っています。

    -   最初の接続が成功したが、インターネット接続が利用できない、モバイル ブロード バンド アプリが起動し、ユーザーを求められますの購入プラン。

    -   最初の接続が失敗し、エラー コードを示しているネットワーク サービスがまだ購入されていません、モバイル ブロード バンド アプリが開始します。 アプリでは、適切な応答を確認できます。 たとえば、エラー コードは、接続がないのためには、アプリが電話で、または別のインターネット接続に接続して、購入を完了するユーザーに指示する必要があります。

    -   最初の接続では、別のエラー コードが失敗した場合、Windows 接続マネージャーには、エラーに関するユーザーに通知します。 モバイル ブロード バンド アプリは開始されません。

6.  モバイル ブロード バンドのアプリを開いたときは、ユーザーがサブスクリプションを購入できるように、バックエンド課金インフラストラクチャをセキュリティで保護された接続を作成するアプリを記述することを確認してください。 このプロセスは各オペレーターの専用と Microsoft は、購入プロセスに関与できません。 アプリでは、この接続や Wi-fi などの別のインターネット接続経由では、(演算子のネットワークを有効にする必要があります) を制限付きのモバイル ブロード バンド接続を確立します。

7.  プランを購入が完了したら、モバイル ブロード バンド アプリは、プロビジョニング、プロビジョニング エージェントに渡されるファイル メタデータを生成します。 これにより、Windows が、ユーザーが購入したプランに関する情報を構成します。

**重要な**  上記の手順は、代替のインターネット接続の PC に接続されている外部のデバイスにも適用されます。

 

### <a name="span-idmobilebroadbandappisnotinstalledandnoalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisnotinstalledandnoalternateinternetconnectionisavailablespanspan-idmobilebroadbandappisnotinstalledandnoalternateinternetconnectionisavailablespanmobile-broadband-app-is-not-installed-and-no-alternate-internet-connection-is-available"></a><span id="Mobile_broadband_app_is_not_installed_and_no_alternate_Internet_connection_is_available"></span><span id="mobile_broadband_app_is_not_installed_and_no_alternate_internet_connection_is_available"></span><span id="MOBILE_BROADBAND_APP_IS_NOT_INSTALLED_AND_NO_ALTERNATE_INTERNET_CONNECTION_IS_AVAILABLE"></span>モバイル ブロード バンド アプリがインストールされていないと、代替のインターネット接続が使用できません。

外部モバイル ブロード バンド デバイス ハードウェアのドングルなどは、使用可能な別のインターネット接続がない可能性があり、モバイル ブロード バンド アプリがインストールされていない可能性がありますを Pc に挿入できます。 次の手順では、このシナリオでの制限を回避するプランの購入エクスペリエンスを構築する方法について説明します。

1.  モバイル ブロード バンド ハードウェアが検出されるとすぐに Windows モバイル ブロード バンド サービスは、IMSI や、ICCID、プロバイダーの ID プロバイダー名を読み取るし、デバイスから読み取られた各値を表す HWIDs のセットを生成します。 Windows モバイル ブロード バンド サービスは、モバイル ブロード バンド関連のイベントをリッスンします。

2.  ユーザーがクリックすると**Connect**HWID 値は、次のように Windows APN データベースの接続設定を検索に使用されます。

    -   最初の接続が成功すると、インターネット接続が利用できる場合は、さらに何も起こりません。 ユーザーは、サービスを購入したが、アクティブなアカウントを持っています。

    -   最初の接続が成功するとインターネット接続が利用できない場合、この HWID 範囲の APN データベースで指定された URL にユーザーが取得されます。

    -   最初の接続が失敗した場合は、Windows 接続マネージャーには、エラーに関するユーザーに通知します。 Web サイトでは、プランの購入にユーザーを支援する必要があります。

3.  ユーザーには、プランの購入が完了すると、web サイトがプロビジョニング ファイルのメタデータを生成し、プロビジョニング エージェントに渡します。 これにより、Windows が、ユーザーが購入したプランに関する基本情報を構成します。 ネットワークの構造によっては、次のいずれかが発生します。

    -   現在の接続でインターネット アクセスをユーザーに許可します。

    -   プロビジョニング ファイルには、切断し、同じネットワークまたはインターネットへのアクセスを提供する別のネットワークに再接続する手順が含まれています。

    この時点では、ユーザーはオンラインです。 これで、インターネット接続が使用可能な Windows はモバイル ブロード バンド ハードウェアが検出しダウンロードし、サービスのメタデータと、モバイル ブロード バンド アプリをインストールします。

4.  SIM またはモバイル ブロード バンド デバイスから計算される HWIDs は WMIS に送信されます。 WMIS では、演算子を識別し、適切なサービス メタデータ パッケージを返します。

5.  Windows では、サービス メタデータを使用して識別し、関連付けられているモバイル ブロード バンドのアプリを Microsoft Store から取得します。 アプリが自動的にインストールし、バック グラウンド イベントの登録します。 Windows 8.1 および Windows 10 で、アプリはスタート画面に自動的にピン留めできません。 ローカル データの使用率カウンターへの対応、演算子の SMS メッセージの受信、Wi-fi ホット スポットに接続する権利チェックの処理などの作業を行うアプリをバック グラウンド イベントを登録できます。 バック グラウンド タスクの詳細が記載されて[バック グラウンド タスクの概要](https://www.microsoft.com/download/details.aspx?id=27411)します。

6.  バック グラウンドのイベントが発生して、アプリが必要な場合より詳細なプロビジョニング ファイルが生成されますプロビジョニング エージェントに渡されます。 これにより、Windows が、ユーザーが購入したプランに関する情報を構成します。

### <a name="connecting-an-active-device"></a>アクティブなデバイスを接続します。

アクティブなモバイル ブロード バンドのプランを使用したデバイスが PC に関連付けられている場合操作は、インターネットに接続試行をリードする点を除いて、購入するときと同様のです。 Windows はモバイル ブロード バンド用のモバイル ブロード バンド アプリを起動したり、携帯電話会社の web サイトに接続します。 代わりに、アプリがバック グラウンドでインストールします。

1.  モバイル ブロード バンド ハードウェアが検出されると、モバイル ブロード バンド サービス、IMSI や、ICCID、プロバイダーの ID プロバイダー名を読み取って HWIDs が生成されます。

2.  ユーザーがクリックすると**Connect**HWID 値は、Windows APN データベース内の適切な接続の設定の検索に使用されます。 アクティブなデバイスの接続が成功とインターネット接続を使用します。

3.  この時点では、ユーザーはオンラインです。 インターネット接続が利用できるようになりました Windows はモバイル ブロード バンド ハードウェアの検出しダウンロードしてインストール サービスのメタデータと、モバイル ブロード バンド アプリ。

Windows 8.1 および Windows 10 に接続できます演算子ネットワークを Windows セットアップ中にアクティブなプランでのモバイル ブロード バンド デバイスが、PC に接続されている場合。 モバイル ブロード バンド ネットワークでは、Wi-fi ネットワークと共に Windows セットアップ中にネットワークの一覧に表示します。 アクティブなデバイスを接続するためのプロセスと同様に、HWID は、検出されたモバイル ブロード バンド ハードウェアに基づいて生成され、Windows APN データベース内の適切な接続の設定の検索に使用します。

### <a name="operator-notifications-and-system-events"></a>Operator Notifications とシステム イベント

ユーザーをアカウントの状態に関する情報を通知するために、モバイル ブロード バンド アプリは、ユーザーはこれと対話していない場合でも、一部のアクティビティを実行する必要があります。 これらのアクティビティには、SMS 演算子またはネットワークが開始した USSD メッセージに、データ制限に近づいていることをユーザーに通知する、ユーザーがデータ プランの有効期限が切れていることが通知およびローミングの状態のユーザーに通知する応答が含まれます。 受信 SMS メッセージ、サービス メタデータ パッケージによって、PC で SMS 機能へのアクセスを許可されている権限を持つアプリを利用できます。

一部の SMS メッセージでは、モバイル ネットワーク オペレーターから直接取得し、モバイル ブロード バンドのアプリを使用してユーザーに表示する必要があります。 演算子の SMS メッセージを受信すると、モバイル ブロード バンド アプリでトースト通知を呼び出すことができます。

エンドユーザーが目にするものではありません演算子メッセージ、モバイル ブロード バンド アプリではこれらを処理および適切に動作できます。 Windows 通知サービスが、最も効率的な直接、アプリの通知チャネルを提供しますが、Windows には、モバイル ブロード バンド ネットワークから受信した SMS および非構造化補助サービス データ (USSD) の通知の使用もサポートしています。

SMS メッセージの処理の詳細が記載されて[開発 SMS アプリ](developing-sms-apps.md)します。 オペレーターへの通知に関する詳細情報が記載[mobile operator notifications とシステム イベントを有効にする](enabling-mobile-operator-notifications-and-system-events.md)します。

1.  モバイル ブロード バンド アプリは通知をオペレーターにアクセスするサービス メタデータを宣言します。 プライベートのバック グラウンド イベントを作成しがインストールされている時のオペレーター通知イベントのアプリを登録します。

2.  アプリでは、プロビジョニングのメタデータを適用する場合は、演算子のメッセージと見なされるすべての SMS、USSD のメッセージの説明が含まれます。

SMS、USSD またはメッセージの受信、時に、モバイル ブロード バンド サービスは、プロビジョニングのメタデータで指定された説明するメッセージを比較します。 解析規則が含まれていますが、モバイル ブロード バンド サービスが、またメッセージを解釈し、データの使用状況に関する情報を更新します。

メッセージが一致するものである場合は、そのモバイル ブロード バンドのアプリのプライベートのバック グラウンド イベントを起動して、システム イベント ブローカーに通知されます。 それ以外の場合は、パブリックの SMS イベントを起動して、システム イベント ブローカーに通知されます。

受信 SMS メッセージに応答するは、モバイル ブロード バンド アプリで含めることが、演算子の例をいくつか次に示します。

-   現在のデータ使用量をすぐに同期

-   ユーザーに通知を表示します。

-   アプリのライブ タイルを更新しています

-   取得と適用するにはプロビジョニングのメタデータが更新されました

**注**   Windows 8、Windows 8.1、および Windows 10 含めないオペレーティング システムを使用して SMS アプリのために SMS メッセージを表示するためにモバイル ブロード バンド アプリまたは演算子が特権アクセスを提供するサード パーティ製の SMS アプリが必要ユーザー。

 

**注**   SMS でのモバイル ブロード バンド アプリの構築のサポートはテキスト メッセージが受信したときに、規制の要件や、特定のベスト プラクティスに準拠する必要がありますエンドユーザーに通知 UI を表示するために必要市場です。

 

モバイル ブロード バンド アプリ、モバイル ネットワーク オペレーターに特権アクセスが与えられている UWP アプリ、UWP アプリ (モバイル ブロード バンド デバイスは、PC に組み込まれています) 場合は、PC OEM が特権アクセスが与えられている使用可能な SMS 機能またはモバイル ブロード バンドデバイス IHV (リムーバブル モバイル ブロード バンド デバイスの場合)。 モバイル ネットワーク オペレーターと PC の OEM (または、モバイル ブロード バンド デバイス IHV) は、サービス メタデータからの特権を持つアプリを指定します。 サービス メタデータの詳細については、次を参照してください。[メタデータを使用して、モバイル ブロード バンド エクスペリエンスを構成する](using-metadata-to-configure-mobile-broadband-experiences.md)します。

### <a name="providing-accurate-usage-and-plan-data"></a>使用状況とプランの正確なデータを提供します。

Windows では、データ使用量と、モバイル ブロード バンド アプリがユーザーのデータ プランの説明に使用できるサブスクリプション マネージャー Api を提供します。 モバイル ブロード バンド アプリは、従量制以外のプランでは、およびオペレーターのネットワークから、更新されたデータ使用量の値と従量制課金データ プランのサイズに関する情報をこの API を更新できます。

Windows はこれらの Api を使用して、ユーザーが設定されているデータの使用状況情報を確認し、コア機能の動作を変更します。 たとえば、Windows Update がのみの自動ダウンロード重要な更新プログラム、ユーザーが従量制課金接続を使用する場合。 使用状況に関する情報も、データ使用量とサブスクリプション マネージャー Api を使用してサード パーティ製アプリからアクセスできます。詳細な使用方法のガイドラインについては、「[ネットワークが従量制課金接続の管理に](https://docs.microsoft.com/previous-versions/windows/apps/hh750310(v=win.10))します。

モバイル ブロード バンド アプリがユーザーへのデータの使用量の通知を維持するために使用する選択できるさまざまな機能のチュートリアルを次に示します。

1.  ローカル データ カウンターは、プロファイルの使用状況が変更されたことをユーザーのデータ制限の 5% 以上の前回の更新以降、演算子から予測します。 5% 増加する数は、ハード コーディングし、モバイル ブロード バンド アプリで行うことができますスリープ状態を解除し、5% の増分に対応するバック グラウンド イベントの使用します。

2.  データ使用量とサブスクリプション マネージャーは、使用率が 5% 増加する数を追跡する Windows コンポーネントです。 これには、ローカルの概算使用量の 5% インクリメントごとにバック グラウンド イベントをトリガーする、システム イベント ブローカーに通知します。

3.  システムのイベント ブローカーは、バック グラウンド イベントを処理するためにモバイル ブロード バンドのアプリを起動します。 (通知を受信などの他のトリガーがありますこれを行う。)モバイル ブロード バンド アプリは、この目的のメソッドが呼び出されたときの対処方法を選択できます。

4.  ユーザーが行われた実際に使用量を検証するオペレーターの課金インフラストラクチャから最新の使用状況情報を取得することによってこのイベントを処理するために、アプリのことをお勧めします。 これは可能性があります、非同期操作、ネットワーク経由であり、モバイル ブロード バンド アプリは、オペレーターの課金インフラストラクチャからこの情報を取得中に遅延に対応できる必要があります。 データ使用状況の追跡に大幅な遅延がある場合、モバイル ブロード バンド アプリは、現在の時刻と、最新のデータ間のギャップを埋めるローカル データのカウンターを照会できます。

5.  オペレーターの課金インフラストラクチャを web クエリが完了したら、モバイル ブロード バンド アプリは Windows に使用可能な最新の使用状況情報を示す更新されたプロビジョニングのメタデータを適用できます。

6.  アプリでは、データの使用状況およびサブスクリプション マネージャー Api で更新された情報を発行します。

7.  Windows コンポーネントと、PC でのサード パーティ製アプリを使用してこの使用状況情報にアクセスできる、 [ **Windows.Networking.Connectivity.ConnectionProfile** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile)クラス。 アプリでは、必要に応じてその動作を調整できます。 たとえば、アプリでは、従量制課金接続で低品質のビデオ ストリームを使用できます。

### <a name="internet-sharing"></a>インターネット共有

どこモバイル ブロード バンド接続をユーザーに提供します。 ただし、すべてのデバイスでは、モバイル ブロード バンド デバイスがあります。 Windows 8.1 および Windows 10 は、Wi-fi 経由で友人や家族のさまざまなデバイスを使用すると、モバイル ブロード バンド接続を共有するユーザーを有効にします。

顧客は、PC 設定でインターネット共有を有効にできます。 多くの人たちは、接続を共有するを参照してくださいおよび SSID、Wi-fi ネットワークのパスワードの変更ができます。

自分のデバイスのもう 1 つのモバイル ブロード バンド接続を使用するお客様の場合は、Windows でもやすくなります。 Windows 8.1 または Windows 10 を実行している WiFi 対応の PC 上のネットワークの一覧を開くだけで、共有デバイスの SSID をクリックして**Connect**します。 Windows では、すべてのデバイスの構成とデバイス間の通信を処理します。

構成し、インターネットの共有で動作するしくみ Windows 8.1 および Windows 10 を管理できる、さまざまな機能のチュートリアルを次に示します。

1.  お客様が自動的にダウンロードされ、PC にインストールされるサービス メタデータ パッケージをアップロードすることでインターネット共有を使用できるかどうかを選択できます。

2.  サービス メタデータを使用して、選択することも、モバイル ブロード バンド アプリして、特定の顧客がテザリングをサポートするデータ プランを購入したかどうか、サービスに対する権利チェックを実行するかどうか。

3.  モバイル ブロード バンド アプリは、ユーザーがインターネット共有を有効ことができるかどうかの Windows に指示するたびに、権利チェックを実行するバック グラウンド イベントを登録します。

4.  プロビジョニングのメタデータの一部として、どの PDP コンテキストおよび同時接続を共有できるデバイスの最大数と同様に、共有データ トラフィックに使用する APN を指定できます。

5.  更新のローカル データの使用状況 Api を使用して、お客様のモバイル ブロード バンド接続を共有する他のデバイスによって使用されたデータの量を表示する場合は、モバイル ブロード バンド アプリでエクスペリエンスを作成できます。

インターネットの共有の詳細については、次を参照してください。[の作成とインターネットの共有エクスペリエンスを構成する](creating-and-configuring-internet-sharing-experiences.md)します。

### <a name="wi-fi-hotspot-authentication"></a>Wi-fi ホット スポット認証

プロビジョニングのメタデータの一部として、モバイル ブロード バンド アプリは、演算子が指定した資格情報を使用してユーザーを認証できるホット スポットを記述できます。 WISPr 1.0 のホット スポットなどがありますか、暗号化されたホット スポットが EAP SIM を使用して、EAP-AKA、またはその他のサポートの EAP メソッド。

Windows は、データ トラフィックを範囲内にこれらのホット スポットについて自動的にオフロードします。 Land 行ベースの Wi-fi 場所に、携帯データ ネットワークからネットワーク トラフィックの負荷を軽減するためにこれを実行する可能性があります。 場合によっては、速度やその場所への携帯データ ネットワークよりも優れたカバレッジに、Wi-fi ホット スポットが増加した可能性があります。

行うことも、モバイル ネットワークよりも小さい優先ホット スポット モバイル ブロード バンド接続がないと、使用できますが、データのオフロードを使用していないときに使用する Windows の利用できるようにします。

### <a name="span-idsetupspanspan-idsetupspanspan-idsetupspansetup"></a><span id="Setup"></span><span id="setup"></span><span id="SETUP"></span>セットアップ

-   モバイル ブロード バンド アプリは、Ssid と認証を含むプロビジョニング ファイルを生成します。 そのユーザーを認証できます WiFi のホット スポットのメカニズムです。 これには、この情報を手動で入力しなくても、ユーザーが回避できます。

-   プロビジョニング エージェントは、プロビジョニングのファイルを解析し、Windows 接続マネージャーに必要な情報を提供します。 使用できる場合に、Windows は自動的にこれらのネットワークに接続します。

### <a name="span-idcredentialgenerationspanspan-idcredentialgenerationspanspan-idcredentialgenerationspancredential-generation"></a><span id="Credential_generation"></span><span id="credential_generation"></span><span id="CREDENTIAL_GENERATION"></span>資格情報の生成

モバイル ブロード バンド アプリを生成またはの接続中に、独自の方法で WISPr 資格情報を取得します。 は、プロビジョニングのメタデータには、特定の資格情報を提供するのではなく、アプリへの参照が含まれます。 特定の資格情報が含まれる場合は、このフェーズはスキップされます。

1.  Wi-fi ホット スポットで専用のポータル サイト web サイトには、ワイヤレス インターネット サービス プロバイダー ローミング (WISPr) プロトコルからのチャレンジが含まれています。

2.  静的な資格情報が指定されなかった場合 Windows 接続マネージャーは、ホット スポット認証が行われているシステム イベント ブローカーを通知します。 それ以外の場合、Windows 接続マネージャーは、認証に直接進みます。

3.  独自の認証スキームは、システムのイベント ブローカーは、資格情報を生成する場合は、モバイル ブロード バンド アプリを呼び出します。

4.  アプリでは、その独自のメカニズムを使用して資格情報を生成します。 これらは、ネットワーク リソース、またはモバイル ブロード バンド インターフェイスのやり取りが発生しない可能性があります。 最終的にアプリには、次の操作のいずれか。

    -   **資格情報を提供**--、アプリのこのネットワークの資格情報の生成し、し、Windows 接続マネージャーに戻すことができます。 Windows 接続マネージャーは、ホット スポットが WISPr を使用して認証します。

    -   **接続のキャンセル**--PC は、このネットワークに接続されていない必要があります。 Windows 接続マネージャーは、接続を終了します。

    -   **認証をキャンセル**-別のメソッドを使用して、アプリが認証されています。 Windows 接続マネージャーは、認証も、接続を切断します。

    -   **ユーザーとの対話**-アプリが前面に移動します。 これは、接続ごとの支払ホット スポットなど、ユーザーの確認が必要なときに選択されます。 アプリが必要があります、ユーザーに通知した後に、上記のいずれかを実行して最終的にします。

### <a name="span-idauthenticationspanspan-idauthenticationspanspan-idauthenticationspanauthentication"></a><span id="Authentication"></span><span id="authentication"></span><span id="AUTHENTICATION"></span>認証

資格情報は、モバイル ブロード バンド アプリ (動的 WISPr 資格情報) によって提供されるか、(静的 WISPr 資格情報、EAP の資格情報) のプロビジョニングの一環として静的に定義されている、Windows は、Wi-fi ホット スポットにこれらの資格情報を提供します。

Windows 接続マネージャーの接続プロファイルをモバイル ブロード バンド アプリによって提供される構成情報は、資格情報の取得方法と配信方法を決定します。 次の手順で、配信が概説されています。

1.  ユーザーは、Wi-fi ホット スポットの範囲では、Windows 接続マネージャーはプロビジョニングのメタデータを使用して静的に定義されている資格情報で応答します。 このデータは、信頼できる web サイトや、モバイル ブロード バンド アプリによって生成できます。

2.  Wi-fi ホット スポットでは、演算子を含む資格情報を検証し、PC がインターネットにアクセスを許可します。

### <a name="displaying-account-information-to-the-user"></a>アカウント情報をユーザーに表示します。

Windows 8、Windows 8.1、および Windows 10 で、サブスクライバーと対話するための最善の方法は、モバイル ブロード バンドのアプリを使用してです。 サブスクライバーの相互作用に関する主要なシナリオに対応することによって、このアプリが開発されます。

1.  Windows では、PC でモバイル ブロード バンド デバイスが検出されるに MNO または MVNO サブスクライバーが属しているを判断します。 オペレーターのサービスのメタデータが一致し、WMIS でを使用してダウンロードします。

2.  サービス メタデータは、Windows 接続マネージャーで、対応するネットワーク エントリにモバイル ブロード バンドのアプリをリンクします。

3.  Windows 接続マネージャーには、オペレーターのロゴ、演算子の名前が表示されると、**アカウントの表示**リンク。

4.  ユーザーは、リンクをクリックすると、モバイル ブロード バンド アプリが開かれます。 課金システムから利用可能な最新の情報を取得するアプリを開発できます。

5.  必要に応じて、アプリは、課金システムが最後に更新されるため、使用量の推定値のローカル データのカウンターを照会できます。 アプリでは、ユーザーの使用状況のほぼリアルタイムの近似を表示するのに、このデータを使用できます。

6.  モバイル ブロード バンド アプリより多くのシナリオを開発できます。 詳細な例とユーザー エクスペリエンスの主なシナリオのモバイル ブロード バンドのアプリを有効にすることができますのガイドラインを参照してください。[モバイル ブロード バンドのアプリのユーザー エクスペリエンスの設計](designing-the-user-experience-of-a-mobile-broadband-app.md)します。

### <a name="enabling-other-devices-and-app-scenarios"></a>その他のデバイスとアプリのシナリオを有効にします。

Windows 8、Windows 8.1、および Windows 10 開発ツールおよびできる柔軟な開発プラットフォームの豊富なセットを提供する、値が強調表示するアプリを作成の利点が一意に決定するサービスを追加します。

### <a name="span-idprivilegedappsspanspan-idprivilegedappsspanspan-idprivilegedappsspanprivileged-apps"></a><span id="Privileged_apps"></span><span id="privileged_apps"></span><span id="PRIVILEGED_APPS"></span>特権のあるアプリ

モバイル ブロード バンド Api とアカウントのプロビジョニングと、SMS などのインターフェイスは、モバイル ブロード バンドのアプリに制限されます。 これらの特権を持つ Api へのアクセス権を持つ特権のあるアプリの一覧は、Windows デベロッパー センター ダッシュ ボードに送信されるサービス メタデータ パッケージで宣言する必要があります。

### <a name="span-idmultiplepdpcontextsspanspan-idmultiplepdpcontextsspanspan-idmultiplepdpcontextsspanmultiple-pdp-contexts"></a><span id="Multiple_PDP_contexts"></span><span id="multiple_pdp_contexts"></span><span id="MULTIPLE_PDP_CONTEXTS"></span>複数の PDP コンテキスト

Windows 8.1 および Windows 10 は、同時にアクティブ化する複数の PDP コンテキストをサポートします。 これにより、携帯を顧客に差別化されたシナリオを提供します。 複数の PDP コンテキストを使用して有効になっているシナリオの詳細については、次を参照してください。[複数の PDP コンテキストを使用してアプリの開発](developing-apps-using-multiple-pdp-contexts.md)します。

### <a name="span-idwirelineoperatorsspanspan-idwirelineoperatorsspanspan-idwirelineoperatorsspanwireline-operators"></a><span id="Wireline_operators"></span><span id="wireline_operators"></span><span id="WIRELINE_OPERATORS"></span>有線演算子

PNP-X 対応を使用して、UWP デバイスのアプリと非モバイル ブロード バンド デバイスを公開することができます。

Dvr、ゲートウェイ ルーターをモバイル ホット スポット、およびスマート フォンは (Windows 8、Windows 8.1、または Windows 10 PC と同じ Wi-fi または LAN ネットワークに接続されている) 中などのデバイスでは、PNP-X 対応を使用して、Windows 8、Windows 8.1、および Windows 10 をその存在に注意してください。 そのデバイスのプロパティに基づいてこれらのデバイスのデバイス メタデータをダウンロードしてで開発した UWP デバイス アプリが自動的にダウンロードします。 1 つのモバイル ブロード バンド アプリはモバイル ブロード バンドとこれらの追加のデバイスを管理できるように、これらのデバイスには、このアプリを参照できます。

## <a name="span-idhowitworksspanspan-idhowitworksspanspan-idhowitworksspanhow-it-works"></a><span id="How_it_works"></span><span id="how_it_works"></span><span id="HOW_IT_WORKS"></span>しくみ


このセクションでは、Windows 8、Windows 8.1、および Windows 10 におけるモバイル ブロード バンドの主なシナリオをサポートするコンポーネントがについて説明します。 Windows オペレーティング システムの一部であるものと、サービスのメタデータまたはモバイル ブロード バンドのアプリの一部であるとは、これらが分割されます。

![オペレーターの操作性を提供するためのコンポーネント](images/mb-overviewtechnicalcomponents.jpg)

### <a name="span-idwindowscomponentsspanspan-idwindowscomponentsspanspan-idwindowscomponentsspanwindows-components"></a><span id="Windows_components"></span><span id="windows_components"></span><span id="WINDOWS_COMPONENTS"></span>Windows コンポーネント

Windows 8、Windows 8.1、および Windows 10 の一部を次のコンポーネントには。

-   [エージェントのプロビジョニング](#provisioning-agent)

-   [データ使用量とサブスクリプション マネージャー](#data-usage-and-subscription-manager)

-   [Windows 接続マネージャー](#windows-connection-manager)

-   [ローカル データのカウンター](#local-data-counters)

-   [モバイル ブロード バンド サービス](#mobile-broadband-service)

-   [モバイル ブロード バンド クラス ドライバー](#mobile-broadband-class-driver)

-   [システム イベント ブローカー](#system-event-broker)

-   [Windows メタデータとインターネット サービス](#windows-metadata-and-internet-services)

-   [Microsoft ストア](#microsoft-store)

### <a name="provisioning-agent"></a>エージェントのプロビジョニング

プロビジョニング エージェントは、Windows ネットワークの設定を構成するためのインターフェイスを提供します。 プロビジョニング エージェントでは、必要な構成を記述する XML ファイルを受け入れます。

次の方法のいずれかでは、XML ファイルを提供できます。

-   署名付き XML ファイルに web サイトによって提供される、 [ **window.external.msProvisionNetworks** ](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/dn529170(v=vs.85))関数以降を実行して、Windows 8、Windows 8.1、または Windows 10 コンピューターで Internet Explorer 10 (または別ブラウザーのサポート)。

-   XML ファイル (符号付きまたは符号なしか) がするアプリによって提供される、 [ **Windows.Networking.NetworkOperators.ProvisioningAgent.ProvisionFromXmlDocumentAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.NetworkOperators.ProvisioningAgent#Windows_Networking_NetworkOperators_ProvisioningAgent_ProvisionFromXmlDocumentAsync_System_String_)関数。

形式とプロビジョニング ファイルの内容に関する詳細については、次を参照してください。[メタデータを使用して、モバイル ブロード バンド エクスペリエンスを構成する](using-metadata-to-configure-mobile-broadband-experiences.md)します。

### <a name="data-usage-and-subscription-manager"></a>データ使用量とサブスクリプション マネージャー

データ使用量とサブスクリプション マネージャーのトラックの詳細、ユーザーのアカウント。 現在接続されているネットワークに関するストアド コスト情報はすべての UWP アプリで使用できます。 プロビジョニング エージェントを使用してこの情報を更新することができます。

通信事業者が、データの使用状況、および要求サブスクリプション マネージャー使用してローカル データ カウンター バック グラウンド イベントをトリガーする場合、データの 5% のときに制限を使用されています。 システムのイベント ブローカーは、このバック グラウンド イベントを提供し、モバイル ブロード バンド アプリは課金対象の使用方法を更新するトリガーとして、イベントを使用することができます。

### <a name="windows-connection-manager"></a>Windows 接続マネージャー

Windows 接続マネージャーは、Wi-fi、モバイル ブロード バンド、およびイーサネットで使用可能なネットワークを監視します。 これは、自動接続し、使用可能なネットワークに基づいた決定を切断します。 プロビジョニング エージェントでは、自分が所有するネットワーク間の相対的な優先順位を定義することができます。 ただし、ユーザーはどのネットワークに手動で接続できます。 Windows 接続マネージャーでは、将来の自動接続の選択に影響を与えるユーザーの手動アクションを使用します。

Windows 接続マネージャーも管理 WISPr 1.0 をサポートする、Wi-fi ホット スポットでの認証の接続後に実行します。 静的な資格情報は、Wi-fi ホット スポットに格納されている、Windows 接続マネージャーが自動的に認証されます。 動的な資格情報が必要な場合は、Windows 接続マネージャーは、システム イベント ブローカーを使用してバック グラウンド イベントをトリガーします。 モバイル ブロード バンド アプリは適切な資格情報を生成する必要がありますし、認証プロセスを完了するために Windows 接続マネージャーを提供します。 詳細については、次を参照してください。[ワイヤレス ホット スポットで統合 Windows](integrating-windows-with-wireless-hotspots.md)します。

### <a name="local-data-counters"></a>ローカル データのカウンター

ローカル データのカウンターは、時間の経過と共に、ネットワーク インターフェイスで送受信されるデータの量を追跡します。 この情報は、複数の場所でユーザーに表示されます。

-   **アプリ履歴**タスク マネージャー タブ

-   (省略可能)Wi-fi またはモバイル ブロード バンド ネットワークの展開ビューに Windows 接続マネージャーです。 ユーザーは、特定のネットワークには、この見積もりを非表示かどうかを決定できます。 既定では、モバイル ブロード バンド ネットワークの表示され、Wi-fi ネットワークを非表示になります。 ただし、Windows では、モバイル ブロード バンド デバイスがインストールされていることを検出する場合、は、対応するモバイル ブロード バンド ネットワークの推定データ使用状況では、Windows 接続マネージャーを非表示されます。 モバイル ブロード バンドのアプリを作成した場合は、ユーザーに表示されるデータの使用法値を制御するしますが、想定があるためにです。 そのために最適な場所は、モバイル ブロード バンド アプリ内です。 ユーザーは、この動作をオーバーライドし、いつでも、ネットワークの推定使用量を表示できます。

ローカル データ カウンターも使用できるプログラムで、次の Api を使用しています。

-   [ **Windows.Networking.Connectivity.ConnectionProfile.GetNetworkUsageAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetNetworkUsageAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_DataUsageGranularity_Windows_Networking_Connectivity_NetworkUsageStates_)関数は、指定した期間データの使用状況を提供します。

-   [ **Windows.Networking.Connectivity.ConnectionProfile.GetConnectivityIntervalsAsync** ](https://docs.microsoft.com/uwp/api/Windows.Networking.Connectivity.ConnectionProfile#Windows_Networking_Connectivity_ConnectionProfile_GetConnectivityIntervalsAsync_Windows_Foundation_DateTime_Windows_Foundation_DateTime_Windows_Networking_Connectivity_NetworkUsageStates_) connect タイムスタンプと期間、ネットワーク インターフェイスを使用する場合、関数が提供します。

ローカル データの使用状況情報は、推定値と、ユーザーのためのガイドとして機能します。 Windows では、同じデータの制限を共有する他のデバイスに対して未請求のトラフィックや使用状況をアカウントことはできません。 たとえば、ファミリは、さまざまなデバイスで同じ SIM を使用してを計画しています。 モバイル ブロード バンド アプリは、およそ使用量の課金システムとの前回の同期以降にのみ、ローカル データのカウンターを使用してください。 既に処理されたデータ使用量の課金システムに従ってください。

### <a name="mobile-broadband-service"></a>モバイル ブロード バンド サービス

モバイル ブロード バンドのサービスは、モバイル ブロード バンド Api とモバイル ブロード バンド デバイス間の通信を管理する Windows サービスです。 サービスは、ドライバーは、Windows モバイル ブロード バンド ドライバー モデルに準拠しているすべてのモバイル ブロード バンド デバイスと対話できます。

サービスは、新しく挿入されたデバイスの SIM の読み取りし、サービス メタデータを取得するプロセスと接続しているモバイル ブロード バンド デバイスに対応するモバイル ブロード バンドのアプリを開始します。

### <a name="mobile-broadband-class-driver"></a>モバイル ブロード バンド クラス ドライバー

モバイル ブロード バンド クラス ドライバーは、その特定のモバイル ブロード バンド デバイス用のカスタム ドライバーを提供するデバイスの製造元の負担を軽減できです。 USB デバイスとしてマニフェストで、USB Implementers Forum に準拠する任意のモバイル ブロード バンド インターフェイス (USB の場合) ネットワーク コントロール モデル (NCM) 2.0 仕様がモバイル ブロード バンド クラス ドライバーによって管理され、追加のドライバーには必要ありませんダウンロードまたはインストールします。

モバイル ブロード バンド クラス ドライバーは、Windows モバイル ブロード バンド ドライバー モデルに適合し、モバイル ブロード バンド サービスへの完全な機能を提供します。 モバイル ブロード バンド アプリに直接公開されるカスタムの拡張機能もサポートしています。 詳細については、次を参照してください。[通信事業者ハードウェア概要](mobile-operator-hardware-overview.md)します。

### <a name="system-event-broker"></a>システム イベント ブローカー

システムのイベント ブローカーは、バック グラウンド イベントを管理します。 システム状態の変化に対応するためにバック グラウンド イベントを受信する、モバイル ブロード バンド アプリを含む、アプリを登録できます。 モバイル ブロード バンド アプリに関心のある可能性があるイベントは次のとおりです。

-   **ネットワークの状態変更**インターネット接続がネットワーク上で変更または – ネットワーク接続または切断します。

-   **アカウントの状態の変更**: 請求サイクルまたは 5% の末尾は、データ使用状況の増分を推定します。

-   **Wi-fi ホット スポット認証**– 必要なパブリックの Wi-fi ホット スポットと資格情報に接続しようとしています。

-   **オペレーターへの着信通知**– 特定の解析中に一致する SMS/USSD メッセージ ルールとして、演算子から SMS/USSD を記述します。

-   **受信した SMS** – オペレーターが定義した解析規則に一致しない SMS メッセージを受信します。

-   **着信 USSD** – オペレーターが定義した解析規則に一致しない USSD メッセージを受信します。

開発者は、対応の厳密な制限がアクティブでないときに、アプリが消費される CPU 時間の上に配置される必要があります。 一部のイベントは、これらの制限が緩やかであり、アプリにする必要があります常に、システムが低電力状態の間、または別のアプリの実行中に使用するリソースが最小化します。 Windows 8 および Windows 10 でのバック グラウンド イベントの詳細については、次を参照してください。[バック グラウンド タスクの概要](https://go.microsoft.com/fwlink/?linkid=227329)します。

### <a name="windows-metadata-and-internet-services"></a>Windows メタデータとインターネット サービス

Windows メタデータとインターネット サービス (WMIS) は、Windows デバイスのエコシステムに参加しているサード パーティからの Windows をカスタマイズを提供するクラウド ベースの Windows サービスです。 モバイル ブロード バンド デバイスの場合は、WMIS は、サービス メタデータ パッケージを提供します。 これは、Windows がモバイル ブロード バンドのアプリを Microsoft Store から取得し、最初に、ネットワークへの接続を許可する、Windows 接続マネージャーで適切なブランド化要素を表示するために必要な基本的な情報を提供します。

### <a name="microsoft-store"></a>Microsoft Store

Microsoft Store は、UWP アプリは、Windows 8、Windows 8.1、および Windows 10 Pc に配信される主な方法です。 モバイル ブロード バンド アプリでは、アプリ パッケージは、デバイスが接続された後、インターネット接続が使用可能な場合に Microsoft Store から取得されます。 アプリ パッケージはその時点で自動的にインストールされていると、ユーザーが使用可能です。 Windows 8.1 および Windows 10 では、アプリがで使用できる**すべてのアプリ**がスタート画面に自動的にピン留めできません。

UWP デバイス アプリの詳細については、次を参照してください。 [UWP デバイス アプリ](https://docs.microsoft.com/windows-hardware/drivers/devapps/index)します。

**注**  企業が特定の条件下で UWP アプリの負荷を側はこれらはいないこのドキュメントで説明します。

 

### <a name="span-idoperatormetadataspanspan-idoperatormetadataspanspan-idoperatormetadataspanoperator-metadata"></a><span id="Operator_metadata"></span><span id="operator_metadata"></span><span id="OPERATOR_METADATA"></span>演算子のメタデータ

演算子に関するメタデータは、以下に示すよう、Windows 8 および Windows 10 の 3 つの方法で提供されます。 各メタデータ オプションは、さまざまな顧客を対象とします。 3 つの種類のメタデータの配信方法と、それぞれどのような情報が使用されるを理解するお客様に対処する際に役立ちます。

演算子のメタデータの詳細については、次を参照してください。[メタデータを使用して、モバイル ブロード バンド エクスペリエンスを構成する](using-metadata-to-configure-mobile-broadband-experiences.md)します。

### <a name="span-idwindowsapndatabasespanspan-idwindowsapndatabasespanspan-idwindowsapndatabasespanwindows-apn-database"></a><span id="Windows_APN_database"></span><span id="windows_apn_database"></span><span id="WINDOWS_APN_DATABASE"></span>Windows APN データベース

Windows APN データベースは、すべての Windows 8、Windows 8.1、および Windows 10 Pc 上に存在します。 データベースは、接続情報の正確性を確保しやすく、Windows Update を使用して、定期的に更新されます。 データベースへの更新は、した要求の処理を行っています。 APN データベースの接続を試みるか APNs やインターネット接続がない場合に、ユーザーが誘導される必要があります URL など、モバイル ブロード バンドのデバイスを検出すると、ネットワークに接続する方法について Windows に情報を提供しますご利用いただけます。

この情報は、モバイル ブロード バンド デバイスの接続の秒以内にオンライン顧客を取得します。 Web ブラウザーを使用してサービスをすぐに購入またはサービスが既に購入した場合にすぐにオンラインが有効にする必要があります。

Windows APN データベースへの更新を送信する方法の詳細については、次を参照してください。 [COSA/APN データベース送信](cosa-apn-database-submission.md)します。

### <a name="span-idservicemetadataspanspan-idservicemetadataspanspan-idservicemetadataspanservice-metadata"></a><span id="Service_metadata"></span><span id="service_metadata"></span><span id="SERVICE_METADATA"></span>サービス メタデータ

サービス メタデータは、モバイル ブロード バンド デバイスを接続した後、すべてのユーザーに配信されます。 従量制課金のモバイル ブロード バンドを含むまたはネットワークをローミング ユーザーがあるのすべてのインターネット接続、限り、サービス メタデータが常に自動的にダウンロードされます。

この情報により、お客様は、Windows 接続マネージャーのブランド化要素を追加することができ、Microsoft Store から自動的に取得したモバイル ブロード バンド アプリを参照している最新のモバイルでより豊富なエクスペリエンスを実現するにはオンラインで購入またはインターネット接続を取得するためのブロード バンド設定します。 Windows は、WMIS から最新のサービス メタデータ パッケージがあることを定期的に確認します。

サービス メタデータ パッケージは、PC で、指定したオペレーターの場合は、モバイル ブロード バンド デバイスが検出された場合にのみ、お客様に配信されます。 存在するときに、このパッケージ内の情報は、APN データベースの内容を上書きします。 サービス メタデータ パッケージ スキーマ リファレンスの詳細については、次を参照してください。[サービス メタデータ パッケージ スキーマ リファレンス](service-metadata-package-schema-reference.md)します。

サービス メタデータ パッケージを作成する方法の詳細については、次を参照してください。[サービス メタデータを作成するための開発者ガイド](developer-guide-for-creating-service-metadata.md)します。

### <a name="span-idprovisioningmetadataspanspan-idprovisioningmetadataspanspan-idprovisioningmetadataspanprovisioning-metadata"></a><span id="Provisioning_metadata"></span><span id="provisioning_metadata"></span><span id="PROVISIONING_METADATA"></span>プロビジョニングのメタデータ

メタデータのプロビジョニングに配信されます、PC、演算子の web サイトまたはモバイル ブロード バンド アプリのいずれかによって、サブスクライバーがサービスを購入した後。 メタデータをプロビジョニングして、XML ファイルとしてパッケージ化は、PC のネットワーク設定を変更するプロビジョニング エージェントによって処理されます。

プロビジョニングのメタデータは、各サブスクリプション会員の個別の要件に対して指定できます。 モバイル ブロード バンドのアプリを使用して、プロビジョニングのメタデータをより高い頻度で更新も可能性があります。 プロビジョニングのメタデータ内の情報は、APN データベースとサービスのメタデータの内容を上書きします。 これに、サブスクライバー情報の最も的調整されたためにです。

 

 





