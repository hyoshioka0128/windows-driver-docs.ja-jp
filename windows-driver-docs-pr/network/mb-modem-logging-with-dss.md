---
title: DSS で MB モデムのログ記録
description: DSS で MB モデムのログ記録
ms.assetid: A40EAF7C-A808-4C2D-848C-EAD2D639EB55
keywords:
- DSS、DSS でログに記録するモバイル ブロード バンド モデムで MB モデムのログ記録
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d9f4869fed3c1929f35520eccc6811d7d24ed7e8
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905370"
---
# <a name="mb-modem-logging-with-dss"></a>DSS で MB モデムのログ記録

## <a name="overview"></a>概要

このトピックでは、Microsoft USB MBIM 1.0 仕様では、Windows 10、1903 およびそれ以降のバージョンで使用可能な拡張機能を使って新しい標準 Windows モバイル ブロード バンド (MBB) のログ記録インターフェイスについて説明します。 

この新しいログ記録のインターフェイスで、OS は、開始、停止、および MBIM CID コマンドを使用して OS ファイル システムにログをフラッシュする MBB デバイスを通知できます。 モデムのログ記録のペイロード、MBB サービスが使用して、OS は MBB データ サービス Stream (DSS) にログ記録のペイロードを送信するデータ チャネルの非 IP の性質です。 DSS がで定義されている、[モバイル ブロード バンド インターフェイス モデル (MBIM) 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)仕様。 

OS には、一連の Windows 固有 MBB ログ構成の全体の MBB エコシステム全体のモデムの診断機能と構成が抽象化します。 これらの MBB ログ記録の構成には、OS MBB ログ記録の要件を適切な内部的なログ記録の構成にマップするモデムの仕入先が有効にします。 抽象化され、OS によって定義されたログの構成には、MBB ログ記録の詳細レベルおよびフラッシュ時間の最大値が含まれます。 

モデムは、セグメントが入力されますと MBIM framework、OS にセグメントを送信するか (セグメントが入力されていない) 場合も同様に、最大のフラッシュの日時に達したときに、バッファーの内容をフラッシュするまで、最大バッファー サイズ、最大のログ バッファーの入力を保持します。 OS は、ログ出力の構成レベル、このトピックの後半で説明されている標準の Windows MBB のセットを定義します。 各構成レベルでは、OS の抽象化 MBB ログの詳細情報と詳細度を指定します。

MBB 構成レベルの OS の抽象化は、モデムで適切な内部のモデムの構成にマップされます。 OS では、ログ記録フィルターなど、OS MBB 構成レベル以外のモデムのマスクの追加の構成ペイロードは提供されません。 

MBB ログ記録をサポートするモデム、ログ出力の構成レベル MBIMLoggingLevelOem を除くすべての MBB がすべての BSP バリアント上に存在する必要があります。 つまり、IHV および OEM する必要があります本番用またはラボ レベルのサポート MBB 運用および BSP の (R & D) のバージョンの両方にログ記録します。 ラボ レベルの MBB のログ記録は、OS からのみ無効にできます。

この新しいログ インターフェイスの設計では、コントロール チャネルを使用して、ログ パラメーターを設定して、データ チャネルがモデムのデータを一括転送するように設計するために、モデムのログを受信するデータ チャネルを使用します。 この設計の利点は、その一括データはデバイスのパフォーマンスの整合性を保つため、コントロール チャネル経由で転送する必要はありません。 またより高いスループットにもスケーリングします。 データ チャネルは、DSS コマンドによって運営されます。 モデムのフローの例は、次のようになります。

1. OS は、MBIM_CID_MODEM_LOGGING_CONFIG CID を MaxSegmentSize、MaxFlushTime、および、LoggingLevel などのログ記録のパラメーターを構成するモデムに送信します。
2. モデムのログ記録、MBIMDssLinkActivate 状態、および一意の DSS セッション id。 特定の GUID でモデムに送信モデムから正常な応答を受信すると、OS MBIM_CID_DSS_CONNECT DSS コマンド
3. 成功状態コードを受信した後、OS は、モデムからフラグメントを受信する準備します。 これらのフラグメントは、DataServiceSessionRead パケットと呼ばれます。
4. DataServiceSessionRead パケットは、OS は、同じ DSS セッション ID と、MBIMDSSLinkDeactivate 状態別 MBIM_CID_DSS_CONNECT コマンドが発行されるまでの到着に進みます。

## <a name="modem-logging-data-path"></a>モデムのログ データのパス

Moddem ログでは、MBIM データ サービス Stream (DSS) を使用して、ログ記録のペイロードのデータを転送します。 DSS の詳細については、の 10.5.38」セクションを参照してください、 [MBIM 1.0 仕様](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。 

接続または DSS から切断すると、次の GUID は、モデムのログ記録の使用されます。

| GUID | 値 |
| --- | --- |
| ModemFileTransfer GUID | 0EBB1CEB-AF2D-484D-8DF3-53BC51FD162C |

次のフロー図は、DSS セットアップと破棄プロセスを示しています。

![DSS は、モデムのログ記録のセットアップと破棄のフロー ダイアグラム](images/mb-modem-logging-dss-flow.png "DSS モデムのログ記録のセットアップと破棄のフロー図。")

## <a name="ndis-interface-extension"></a>NDIS インターフェイスの拡張機能

次の OID は Windows 10、バージョンが 1903、モデムのログ記録をサポートするために定義されています。

- [OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| サービス名 | UUID | UUID 値 |
| --- | --- | --- |
| Microsoft Basic IP 接続の拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-9d3a-bef7058e9aaf |

次の表に、UUID を指定して、各 CID のコードをコマンドだけでなく、CID がサポートしているかどうかを設定、クエリ、またはイベント (通知) を要求します。 詳細については、パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個々 のセクションを参照してください。 

| CID | UUID | コマンド コード | 設定 | クエリ | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MODEM_LOGGING_CONFIG | UUID_BASIC_CONNECT_EXTENSIONS | TBD | Y | Y | Y |

## <a name="mbimcidmodemloggingconfig"></a>MBIM_CID_MODEM_LOGGING_CONFIG

この CID は、モデムとどのくらいの頻度がモデムからホストに送信、DSS 経由で収集されるログの構成に使用されます。 ログ セッションを開始する前に、ログ記録を構成する必要があります。 この CID がの一部であるため、拡張機能の接続はこの CID をサポートするために Ihv を省略できます。 IHV は、DSS データ チャネル経由でモデムのログ記録をサポートする場合、機能として指定にする必要があります。 MBIM_BASIC_CID_DEVICE_SERVICES CID を使用して、機能を提供できます。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MODEM_LOGGING_CONFIG | 適用不可能 | 該当なし |
| 応答 | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG |

### <a name="query"></a>クエリ

現在のモデムのログの構成を照会します。 MBIM_COMMAND_MSG の InformationBuffer は使用されません。 次の MBIM_MODEM_LOGGING_CONFIG 構造は、MBIM_COMMAND_DONE InformationBuffer に使用されます。

#### <a name="mbimmodemloggingconfig"></a>MBIM_MODEM_LOGGING_CONFIG

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | バージョン | UINT32 | この構造体のバージョン番号。 このフィールドを設定する必要があります**1**この構造体のバージョン 1。 |
| 4 | 4 | MaxSegmentSize | UINT32 | モデムが送信される各フラグメントをキロバイト単位では、セグメントのサイズを指定します。 デバイス サービス コマンドのモデムがサポートされている最大のフラグメント サイズが設定された値を超えている場合、この値は、サポートされているセグメントの最大サイズに設定されます。 |
| 8 | 4 | MaxFlushTime | UINT32 | 最大の時刻を示す時間 (ミリ秒単位)、ログのフラグメントを送信する前に、モデムが待機します。 収集されたログに到達しない場合**MaxSegmentSize**内、 **MaxFlushTime**期間のサイズに関係なくログ フラグメントを送信し、ログの最後のフラグメントが送信されるためです。 ログ データがない場合は、通知は送信されません。 デバイスは、短期間のフラッシュを処理できない場合、デバイスは、応答で処理できる時刻を返します。 クエリまたはセットへの応答が含まれていますが、現在構成されている**MaxFlushTime**します。 |
| 12 | 4 | LevelConfig | MBIM_LOGGING_LEVEL_CONFIG | ログの収集対象のレベルを構成します。 クエリまたはセットへの応答が含まれていますが、現在構成されている**LevelConfig**します。 |

> [!NOTE]
> モデムに、要求された OS にログ データを提供することがない場合**MaxSegmentSize**と**MaxFlushTimer**、これらのパラメーターの独自の値を選択し、セットの応答として OS の更新、または要請されていないイベントです。 場合、OS の動作は変更されません**MaxSegmentSize**または**MaxFlushTimer**に関係なくデータ パケットを受信し、それらをファイルにダンプを変更します。

次の MBIM_LOGGING_LEVEL_CONFIG 列挙型は、前述の MBIM_MODEM_LOGGING_CONFIG 構造で使用されます。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMLoggingLevelProd | 0 | 製品版または運用環境の作成からのテレメトリの収集対象としています。 結果のログは capsule 規模にする必要があり、キーのモデムまたは MBB 状態または失敗の情報のみが含まれています。 |
| MBIMLoggingLevelLabVerbose | 1 | 成熟度を MBB 製品の開発を対象としています。 モデムの詳細のフルスタック キャプチャします。 結果として得られるモデム キャプチャには、IHV を再生し、ログの中に、キャプチャを完全に回復が有効にする必要があります。 |
| MBIMLoggingLevelLabMedium | 2 | 検証およびフィールドが相対の成熟度や安定性と MBB 製品のテストの対象としています。 詳細と詳細度のレベルでは、ほとんどの MBB 障害のトリアージを IHV エンジニアのための十分なデータ ポイントを提供します。 |
| MBIMLoggingLevelLabLow | 3 | 自己ホスト レベルのログ記録の対象としています。 フル スタックのキャプチャのモデムの概要レベルのキャプチャ。 モデムの状態と OS の相互作用を強調表示のレベルの理解を有効にします。 |
| MBIMLoggingLevelOem | 4 | OEM および IHV は内部使用に予約されています。 |

### <a name="set"></a>Set

Set コマンドは、レベル、セグメントのサイズとフラッシュする最大時間をモデムのログ記録を構成する設定に使用されます。 MBIM_MODEM_LOGGING_CONFIG 構造体は、InformationBuffer で使用されます。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には MBIM_MODEM_LOGGING_CONFIG 構造体が含まれています。

### <a name="unsolicited-events"></a>要請されていないイベント

要請されていないイベントは、モデムが内部変更について、OS に通知する必要があるシナリオでサポートされます。 現時点では、Windows 10、バージョンが 1903 年でこれらのシナリオは発生しません。

### <a name="status-codes"></a>状態コード

この CID がのみの 9.4. 5. のセクションで定義された汎用的なステータス コードを使用して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。

## <a name="dss-session-behavior-during-inactivity"></a>非アクティブ時の DSS セッションの動作

次の表では、非アクティブのさまざまな段階で DSS セッションの動作方法について説明します。

| シナリオ | DSS セッションの状態 |
| --- | --- |
| システム スリープ、モデム専用のスリープ状態、リセット、および回復 | DSS セッションが開かれたまま |
| システムのシャット ダウン、再起動、休止状態 | DSS セッション終了済み |
