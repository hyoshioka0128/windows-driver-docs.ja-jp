---
title: DSS による MB モデムのログ記録
description: DSS による MB モデムのログ記録
ms.assetid: A40EAF7C-A808-4C2D-848C-EAD2D639EB55
keywords:
- DSS を使用した MB モデムのログ記録 (DSS を使用したモバイルブロードバンドモデムのログ記録)
ms.date: 03/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 065aaf77f225ecbbbe199083f1006910168ee917
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557719"
---
# <a name="mb-modem-logging-with-dss"></a>DSS による MB モデムのログ記録

## <a name="overview"></a>概要

このトピックでは、Windows 10 バージョン1903以降で使用できる、USB MBIM 1.0 仕様の Microsoft 拡張機能を使用した標準の Windows mobile ブロードバンド (MBB) の新しいログインターフェイスについて説明します。 

この新しいログ記録インターフェイスにより、OS は MBB デバイスに対し、MBIM CID コマンドを使用して、OS ファイルシステムへのログの開始、停止、およびフラッシュを通知することができます。 モデムのログペイロードの IP 以外の性質上、MBB サービスがログペイロードを OS に転送するために使用するデータチャネルは、MBB Data Service Stream (DSS) を使用します。 DSS は、[モバイルブロードバンドインターフェイスモデル (MBIM) 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)仕様で定義されています。 

OS は、一連の Windows 固有の MBB ログ構成を使用して、MBB エコシステム全体にわたってモデムの診断機能と構成を抽象化します。 これらの MBB logging 構成により、モデムのベンダーは OS MBB logging の要件を適切な内部ログ構成にマップできます。 OS によって抽象化および定義されたログ構成には、MBB logging の詳細レベルと最大フラッシュ時間が含まれます。 

モデムは、セグメントがいっぱいになるまで、最大バッファーサイズまでログバッファーをいっぱいにします。また、MBIM フレームワークはそのセグメントを OS に送信します。また、最大フラッシュ時間に達すると (セグメントがいっぱいになっていない場合でも)、バッファーの内容をフラッシュします。 OS では、このトピックの後半で説明する標準の Windows MBB logging 構成レベルのセットを定義します。 各構成レベルは、MBB logging details と詳細度の OS 抽象化を指定します。

MBB config レベルの OS 抽象化は、モデムによって適切な内部モデム構成にマップされます。 Os MBB の構成レベル以外のモデムには、ログフィルターやマスクなどの追加の構成ペイロードが提供されません。 

MBB のログ記録をサポートするモデムの場合、MBIMLoggingLevelOem を除く MBB ログのすべての構成レベルは、すべての BSP バリアントに存在する必要があります。 つまり、IHV または OEM は、MBB logging の製品またはラボレベルを、運用環境と R&D バージョンの BSP の両方でサポートする必要があります。 MBB ログのラボレベルは、OS からのみ無効にすることができます。

この新しいログ記録インターフェイスの設計では、コントロールチャネルを使用してログパラメーターを設定し、データチャネルは一括モデムデータを転送するように設計されているため、データチャネルを使用してモデムログを受信します。 この設計の利点は、一括データを制御チャネルを介して転送する必要がないため、デバイスのパフォーマンスが一貫して維持されることです。 さらに、スループットを向上させることができます。 データチャネルは、DSS コマンドによって操作されます。 モデムのフローの例は次のようになります。

1. OS は MBIM_CID_MODEM_LOGGING_CONFIG CID をモデムに送信して、MaxSegmentSize、MaxFlushTime、Logginglevel.information などのログパラメーターを構成します。
2. OS は、モデムから正常な応答を受信すると、モデムログ用の特定の GUID、MBIMDssLinkActivate 状態、および一意の DSS セッション ID を使用して、MBIM_CID_DSS_CONNECT DSS コマンドをモデムに送信します。
3. 成功の状態コードを受信すると、OS はモデムからフラグメントを受信する準備をします。 これらのフラグメントは DataServiceSessionRead パケットと呼ばれます。
4. OS が同じ DSS セッション ID と MBIMDSSLinkDeactivate 状態を持つ別の MBIM_CID_DSS_CONNECT コマンドを発行するまで、DataServiceSessionRead パケットは引き続き到着します。

## <a name="modem-logging-data-path"></a>モデムのログデータのパス

Moddem のログ記録では、MBIM Data Service Stream (DSS) を使用して、ログペイロード用にデータを転送します。 DSS の詳細については、「 [Mbim 1.0 仕様](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)の10.5.38」セクションを参照してください。 

DSS との接続または切断を行う場合、次の GUID がモデムのログ記録に使用されます。

| GUID | 値 |
| --- | --- |
| モデム Filetransfer GUID | 0EBB1CEB-AF2D-484D-8DF3-53BC51FD162C |

次のフロー図は、DSS のセットアップと破棄プロセスを示しています。

![DSS モデムログセットアップと破棄フローダイアグラム](images/mb-modem-logging-dss-flow.png "DSS モデムログのセットアップおよび破棄フローダイアグラム。")

## <a name="ndis-interface-extension"></a>NDIS インターフェイス拡張

次の OID は、Windows 10 バージョン1903でモデムのログ記録をサポートするように定義されています。

- [OID_WWAN_MODEM_LOGGING_CONFIG](oid-wwan-modem-logging-config.md)

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| [サービス名] | UUID | UUID の値 |
| --- | --- | --- |
| Microsoft 基本 IP 接続拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-9d3a-bef7058e9aaf |

次の表では、各 CID の UUID とコマンドコードに加えて、CID が Set、Query、または Event (通知) 要求をサポートしているかどうかを示します。 パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個別のセクションを参照してください。 

| CID | UUID | コマンドコード | オン | クエリ | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_MODEM_LOGGING_CONFIG | UUID_BASIC_CONNECT_EXTENSIONS | TBD | Y | Y | Y |

## <a name="mbim_cid_modem_logging_config"></a>MBIM_CID_MODEM_LOGGING_CONFIG

この CID を使用して、モデムによって収集されるログと、それらが DSS 経由でモデムからホストに送信される頻度を構成します。 ログセッションを開始する前にログを構成する必要があります。 この CID は connect 拡張機能の一部であるため、Ihv がこの CID をサポートするためのオプションです。 IHV が DSS データチャネルを介したモデムのログ記録をサポートしている場合は、これを機能として指定する必要があります。 この機能は MBIM_BASIC_CID_DEVICE_SERVICES CID を使用して提供できます。

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MODEM_LOGGING_CONFIG | 適用外 | 適用なし |
| 応答 | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG | MBIM_MODEM_LOGGING_CONFIG |

### <a name="query"></a>クエリ

現在のモデムログの構成を照会します。 MBIM_COMMAND_MSG の InformationBuffer は使用されません。 次の MBIM_MODEM_LOGGING_CONFIG 構造は、MBIM_COMMAND_DONE の InformationBuffer で使用されます。

#### <a name="mbim_modem_logging_config"></a>MBIM_MODEM_LOGGING_CONFIG

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | Version | UINT32 | この構造体のバージョン番号。 この構造体のバージョン1では、このフィールドを**1**に設定する必要があります。 |
| 4 | 4 | MaxSegmentSize | UINT32 | モデムによって送信される各フラグメントのセグメントサイズをキロバイト単位で指定します。 [デバイスサービス用のモデム] コマンドでサポートされる最大フラグメントサイズが値を超えている場合、この値はサポートされているセグメントの最大サイズに設定されます。 |
| 8 | 4 | MaxFlushTime | UINT32 | モデムがログフラグメントを送信するまでに待機する最大時間をミリ秒単位で示します。 最後のログフラグメントが送信されてから**Maxflushtime**期間内に収集されたログが**MaxSegmentSize**に届かない場合は、そのサイズに関係なくログフラグメントが送信されます。 ログデータがない場合、通知は送信されません。 デバイスがより小さなフラッシュ時間を処理できない場合、デバイスは応答で処理できる時間を返します。 クエリまたはセットに対する応答には、現在構成されている**Maxflushtime**が含まれます。 |
| 12 | 4 | LevelConfig | MBIM_LOGGING_LEVEL_CONFIG | ログを収集するレベルを構成します。 クエリまたはセットに対する応答には、現在構成されている**Levelconfig**が含まれています。 |

> [!NOTE]
> モデムが、要求された**MaxSegmentSize**および**maxflushtimer**で os にログデータを提供できない場合は、これらのパラメーターに対して独自の値を選択し、set 応答または要請されていないイベントとして os を更新できます。 **MaxSegmentSize**または**maxflushtimer**が変更されても、OS の動作は変更されません。これは、データパケットがに関係なく受信され、ファイルにダンプされるためです。

前の MBIM_MODEM_LOGGING_CONFIG 構造体では、次の MBIM_LOGGING_LEVEL_CONFIG 列挙体が使用されます。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| Mbimログインレベルの生産 | 0 | 製品または製品の作成からのテレメトリ収集を目的としています。 生成されるログは、カプセルサイズで、キーモデムまたは MBB の状態またはエラー情報のみが含まれている必要があります。 |
| Mbimの Levellabverbose | 1 | 成熟度の低い MBB 製品の開発を目的としています。 モデムの詳細なフルスタックキャプチャ。 結果として得られるモデムキャプチャでは、IHV がログの再生中にキャプチャを再生し、完全に復旧できるようにする必要があります。 |
| Mbimの Levellabmedium | 2 | 相対的な成熟度と安定性を備えた MBB 製品の検証とフィールドテストを目的としています。 詳細レベルと詳細度は、IHV エンジニアがほとんどの MBB エラーをトリアージするのに十分なデータポイントを提供します。 |
| Mbimの Levellablow | 3 | 自己ホストレベルのログ記録を目的としています。 フルスタックキャプチャモデムの概要レベルのキャプチャ。 モデムの状態と OS の相互作用を強調表示レベルで理解できるようにします。 |
| MBIMLoggingLevelOem | 4 | OEM および IHV の内部使用のために予約されています。 |

### <a name="set"></a>オン

Set コマンドを使用して、モデムログのレベル、セグメントサイズ、最大フラッシュ時間を構成するように設定します。 InformationBuffer では、MBIM_MODEM_LOGGING_CONFIG 構造体が使用されます。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer に MBIM_MODEM_LOGGING_CONFIG 構造体が含まれています。

### <a name="unsolicited-events"></a>一方的なイベント

要請されていないイベントは、モデムが内部の変更について OS に通知する必要がある場合にサポートされます。 現時点では、Windows 10 バージョン1903では、これらのシナリオは発生しません。

### <a name="status-codes"></a>状態コード

この CID は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション9.4.5 で定義されている汎用ステータスコードのみを使用します。

## <a name="dss-session-behavior-during-inactivity"></a>非アクティブ時の DSS セッション動作

次の表では、非アクティブ状態のさまざまな段階で DSS セッションがどのように動作するかを説明します。

| シナリオ | DSS セッション状態 |
| --- | --- |
| システムスリープ、モデムのみのスリープ、リセットと回復 | DSS セッションを開いたままにする |
| システムのシャットダウン、再起動、休止状態 | DSS セッションが終了しました |
