---
title: 通信事業者の通知のシナリオ
description: 通信事業者の通知のシナリオ
ms.assetid: 3749d9ab-3dff-4216-a23b-0e75c04d9a22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e3f15beb3013c2628437c57a1c38464a75a1d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391971"
---
# <a name="mobile-operator-notification-scenarios"></a>通信事業者の通知のシナリオ


このトピックで説明するシナリオは、通信事業者の通知、モバイル ブロード バンド アプリで使用するとします。

-   [接続し、モバイル ブロード バンドから切断](#conndis)

-   [ネットワーク オペレーター メッセージ](#netopmsg)

-   [データの使用状況をトリガーして、通知をローカルのローミング](#trigloc)

-   [データ プランの有効期限と使用状況のリセット](#expire)

-   [権利チェック インターネット共有](#sharing)

## <a name="span-idconndisspanspan-idconndisspanconnect-to-and-disconnect-from-mobile-broadband"></a><span id="conndis"></span><span id="CONNDIS"></span>接続し、モバイル ブロード バンドから切断


Windows 接続マネージャーは、Wi-fi、モバイル ブロード バンド、およびイーサネットで使用可能なネットワークを監視します。 これは、自動接続し、使用可能なネットワークに基づいた決定を切断します。 Windows 接続マネージャーに接続し、モバイル ブロード バンド プロファイルから切断したときに、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)バック グラウンド イベントをトリガーします。 このイベントは、ユーザーがアカウントの状態を確認する、最新のデータ使用量を取得する通知を表示するなど、ネットワークに接続するときに必要なロジックを実行して、タイルの更新プログラムをモバイル ブロード バンド アプリです。

## <a name="span-idnetopmsgspanspan-idnetopmsgspannetwork-operator-messages"></a><span id="netopmsg"></span><span id="NETOPMSG"></span>ネットワーク オペレーター メッセージ


Windows 8、Windows 8.1、および Windows 10 でのモバイル ブロード バンド プラットフォームを受信し、SMS、USSD 管理用の受信メッセージを表示するためのモバイル ブロード バンド アプリでのみ使用可能な拡張機能を提供します。 これらのメッセージは、ユーザーに通知やデータ使用量が上限、海外ローミング、低い残高に近づいているなど、モバイル ブロード バンド アプリからの応答のトリガーに使用できます。

アプリでは、適切な受信メッセージを処理します。 回答の候補がでは、いずれかまたは次のすべてを含めます。

-   現在のデータ使用量をすぐに同期

-   モバイル ブロード バンド アプリのタイルを更新しています

-   取得と適用演算子プロビジョニング XML を更新

-   ユーザーに通知を表示します。

アプリによってトリガーされるバック グラウンド タスクでメッセージを表示する場合、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントのメッセージの内容を読み取るし、アプリの独自のローカル データ ストレージにメッセージの内容を格納する必要があります。 モバイル ブロード バンド SMS プラットフォームの管理用の SMS 通知を受信したキューを維持しません。

### <a name="span-idmobilenetworkoperatorsmsnotificationsspanspan-idmobilenetworkoperatorsmsnotificationsspanspan-idmobilenetworkoperatorsmsnotificationsspanmobile-network-operator-sms-notifications"></a><span id="Mobile_network_operator_SMS_notifications"></span><span id="mobile_network_operator_sms_notifications"></span><span id="MOBILE_NETWORK_OPERATOR_SMS_NOTIFICATIONS"></span>モバイル ネットワーク オペレーター SMS 通知

受信 SMS メッセージが要求され、コンピューターの SMS 機能へのアクセスを許可されているすべてのアプリを利用できます。 ただし、一部の SMS メッセージ、運送業者から直接取得する必要がありますに制限および、モバイル ブロード バンド アプリによって処理します。

モバイル ブロード バンド SMS プラットフォームは、2 種類のいずれかに新しい各受信した SMS をフィルター処理: モバイル ネットワーク オペレーター (MNO)、および一般的な SMS メッセージを (サイレント) SMS 通知を管理します。 MNO から受信した SMS 通知を管理は、モバイル ブロード バンド アプリにアクセスできるのみ、一般的な SMS クライアント アプリは表示されません。

MNOs は、アカウントのプロビジョニングのメタデータの管理用の SMS、USSD 通知のカスタムのフィルタ リング規則を指定します。 メッセージのフィルタ リング規則が指定されていない場合、SMS プラットフォームはすべてのアプリに使用できる一般的な SMS メッセージとしてすべての SMS メッセージを分類します。 入力方向の SMS プロビジョニング済みのフィルタ リング規則に一致する場合、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントがトリガーされ、バック グラウンド作業項目は受信 SMS メッセージを処理できます。

### <a name="span-idnetwork-initiatedussdspanspan-idnetwork-initiatedussdspanspan-idnetwork-initiatedussdspannetwork-initiated-ussd"></a><span id="Network-initiated_USSD"></span><span id="network-initiated_ussd"></span><span id="NETWORK-INITIATED_USSD"></span>ネットワークが開始した USSD

Windows 8、Windows 8.1、および Windows 10 アプリ開発を簡略化の詳細のほとんどを非表示にする、基になる USSD プロトコルの抽象化であるを USSD API に提供します。 フィルタ リング規則のプロビジョニングと一致するネットワークが開始した USSD を受信すると、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントをトリガーし、対応するバック グラウンド作業項目を使用して、USSD セッション経由で通信できます、USSD API です。

USSD Api の詳細については、次を参照してください。 [ **Windows.Networking.NetworkOperators** ](https://msdn.microsoft.com/library/windows/apps/br241148)名前空間。

## <a name="span-idtriglocspanspan-idtriglocspantriggering-data-usage-and-roaming-notifications"></a><span id="trigloc"></span><span id="TRIGLOC"></span>データの使用状況をトリガーして、通知のローミング


多くの領域で、ユーザーが、データ使用量の制限に達したかがよりコストのかかるネットワークでのローミング ユーザーに通知する法規制によって MNOs が必要です。 このコンシューマー protection には、過剰な使用料金のリスクが軽減されます。 、Windows では、モバイル ブロード バンド アプリはトースト通知を表示して、ユーザーをデータの使用状況と状態のローミングを認識させる更新プログラム タイルします。 これらの通知から実行できるバックエンド ネットワークは、SMS、USSD、またはを使用してトリガーする、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。 または、MobileOperatorNotification イベントは、次の場合にローカルの情報を使用してトリガーできます。

### <a name="span-iddatausagenotificationbyusinglocaldatacountersspanspan-iddatausagenotificationbyusinglocaldatacountersspanspan-iddatausagenotificationbyusinglocaldatacountersspandata-usage-notification-by-using-local-data-counters"></a><span id="Data_usage_notification_by_using_local_data_counters"></span><span id="data_usage_notification_by_using_local_data_counters"></span><span id="DATA_USAGE_NOTIFICATION_BY_USING_LOCAL_DATA_COUNTERS"></span>ローカル データのカウンターを使用してデータの使用状況の通知

1.  プロビジョニングのメタデータを使用してローカル データの使用状況の通知が有効にします。

2.  ローカル データ カウンターは、前回の更新以降、ユーザーのデータ制限の 5% 以上のプロファイルの使用量が変更されたことを予測します。

3.  データ使用量とサブスクリプション マネージャー (DUSM) に通知をトリガーする、システム イベント ブローカー、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。

4.  システムのイベント ブローカーは、バック グラウンド イベントを処理するためにモバイル ブロード バンドのアプリを起動します。

5.  アプリは、バック エンド インフラストラクチャから最新の使用状況情報を取得することによって、イベントを処理します。

6.  現在の使用状況情報は、(80%) などのしきい値を超えている場合、アプリは、トースト通知をユーザーに表示し、現在の使用状況と、DUSM を更新します。 または、現在の使用率がしきい値を超えない場合、アプリがトースト通知を表示する必要はありません。

### <a name="span-idroamingnotificationbyusingwindowsconnectionmanagerspanspan-idroamingnotificationbyusingwindowsconnectionmanagerspanspan-idroamingnotificationbyusingwindowsconnectionmanagerspanroaming-notification-by-using-windows-connection-manager"></a><span id="Roaming_notification_by_using_Windows_Connection_Manager"></span><span id="roaming_notification_by_using_windows_connection_manager"></span><span id="ROAMING_NOTIFICATION_BY_USING_WINDOWS_CONNECTION_MANAGER"></span>Windows 接続マネージャーを使用して通知をローミング

1.  Windows 接続マネージャーのローミング モバイル ブロード バンド ネットワークに登録します。

2.  Windows 接続マネージャーに通知をトリガーする、システム イベント ブローカー、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。

3.  システムのイベント ブローカーは、バック グラウンド イベントを処理するために、通信事業者アプリを起動します。

4.  このネットワークでのローミング中に、ユーザーで追加の使用料金が発生するかどうかと、必要に応じてがユーザーにトースト通知とタイルの更新プログラムを表示するかどうか、アプリを識別します。

## <a name="span-idexpirespanspan-idexpirespandata-plan-expiration-and-usage-reset"></a><span id="expire"></span><span id="EXPIRE"></span>データ プランの有効期限と使用状況のリセット


DUSM 追跡の詳細については、ユーザーのアカウントまたは事前有料データ プランのプランの有効期限の日付を含む、アカウントまたはプランの使用量が後に有料データ プランの日をリセットします。 ユーザーのデータ プランの有効期限、DUSM に通知をトリガーする、システム イベント ブローカー、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。 モバイル ブロード バンド アプリでは、トースト通知を表示して、イベントを処理でき、タイルをユーザーに、プランの有効期限が切れていることを通知またはそのサービスの更新を更新することができます。

後の有料データ プランの場合、DUSM をゼロ、1 か月の最初の曜日など、特定の日付にプランのデータ使用量がリセットされます。 これが発生したときに、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベントがトリガーされ、アプリが更新されたデータの使用量のユーザーに通知できます。

## <a name="span-idsharingspanspan-idsharingspanentitlement-check-for-internet-sharing"></a><span id="sharing"></span><span id="SHARING"></span>権利チェック インターネット共有


Windows 8.1 のインターネット共有をテザリングとも呼ばに追加された 1 つまたは複数の他のいないデバイスをモバイルでのモバイル ブロード バンド ネットワーク接続を共有するユーザーを有効にするブロード バンド対応します。 Bluetooth、USB ケーブルの従来のメカニズムが含まれます。 ただし、Wi-fi できます提供、高速、簡単にモバイル ブロード バンド接続構成はほとんど必要があるために、個人用のホット スポット、モバイル ホット スポットなどのメカニズムを共有により、高速データ転送、および使い慣れた Wi-fi に依存しています接続するプロセス。

一部 MNOs または MVNOs では、ネットワークにインターネットの共有機能はサポートしてまたはインターネットの共有接続をセットアップする前に、権利チェックが必要です。 Windows では、Windows デバイスがネットワーク ポリシーに準拠していることを確認するために必要なコントロールを提供します。 携帯電話会社を設定した場合、 [AllowTethering](allowtethering.md)要素**EntitlementCheckRequired**システムをトリガーするサービス メタデータ パッケージで、 [MobileOperatorNotification](mobile-operator-notification-event-technical-details.md)イベント。 モバイル ブロード バンド アプリは、ユーザーがインターネットの共有機能の使用が許可され、システムに戻す応答かどうかを確認するネットワーク サービスと通信します。 ユーザーが許可された、機能を使用して、インターネットの共有が正常に開始されます、既定のエラー メッセージ、または携帯電話会社によって定義されたメッセージをユーザーに表示されるそれ以外の場合。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Mobile operator notifications とシステム イベントを有効にします。](enabling-mobile-operator-notifications-and-system-events.md)

[作成とインターネットの共有エクスペリエンスの構成](creating-and-configuring-internet-sharing-experiences.md)

 

 






