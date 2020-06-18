---
title: MB SAR プラットフォームのサポート
description: MB SAR プラットフォームのサポート
ms.date: 05/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 05a43b54916dbfef9c96b30c06c7571544906956
ms.sourcegitcommit: f4f861a9f833ef1389ff5c08e2b9de0d3df81bef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84974150"
---
# <a name="mb-sar-platform-support"></a>MB SAR プラットフォームのサポート

## <a name="overview"></a>概要

従来、Oem は、特定の吸収率 (SAR) に対して独自のソリューションを実装していました。 これには、OEM は、ユーザーモードドライバー (UMDF) とモデムの間でのみ識別されるデバイスサービスコマンドを実装するか、またはカーネルモードコンポーネントが直接モデムと対話する必要があります。 一部の Oem は、UMDF モデムコンポーネントとカーネルモードモデムコンポーネントの両方を備えたハイブリッドソリューションを持つこともできます。 無線放射線の認識が増すにつれて、SAR コマンドを通過するように OEM ソフトウェアコンポーネントのインターフェイスを標準化すると、次のような利点があります。

1.  Oem は、ユーザーモードのコンポーネントに移動してシステムの安定性を高めることができます。これは、ユーザーモードでのエラーがカーネルモードと比較してシステムにとって致命的ではないためです。
2.  Windows には、プラットフォーム標準のインターフェイスが用意されており、Oem からの独自の実装が減少します。
3.  SAR を利用するプラットフォームのサービスでは、モデムから情報を取得できます。

Windows 10 バージョン1703以降では、Windows は SAR 構成とモデム転送状態のパススルーをサポートしています。 Windows は引き続き、SAR ビジネスロジックを自己差別化要因として使用しますが、プラットフォームを効率化するインターフェイスを提供します。 このインターフェイスをサポートするために、2つの新しい NDIS Oid と2つの新しい MBIM Cid が定義されています。 OS サポートを利用するデバイスでは、両方のコマンドを実装する必要があります。

この機能は、2つの新しい Oid と Cid にを追加することによってサポートされています。 MBIM を実装する IHV パートナーの場合は、CID バージョンのみをサポートする必要があります。

> [!NOTE]
> このトピックでは、モデムデバイスドライバーに SAR プラットフォームサポートを実装するための IHV パートナー向けのインターフェイスを定義します。 デバイスの SAR マッピングテーブルをカスタマイズする方法の詳細については、「[特定の吸収率 (sar) マッピングテーブルをカスタマイズする](https://docs.microsoft.com/windows-hardware/customize/desktop/customize-sar-mapping-table)」を参照してください。

## <a name="mb-interface-update-for-sar-platform-support"></a>SAR プラットフォームサポート用の MB インターフェイス更新プログラム

MBIM 準拠のデバイスは、CID_MBIM_DEVICE_SERVICES によって照会されたときに、次のデバイスサービスを実装して報告します。 既知の既存のサービスは、USB NCM MBIM 1.0 仕様のセクション10.1 で定義されています。 Microsoft はこれを拡張して次のサービスを定義します。

サービス名 = **MICROSOFT SAR コントロール**

UUID = **UUID_MS_SARControl**

UUID 値 = **68223D04-9F6C-4E0F-822D-28441FB72340**

| CID | 最小 OS バージョン |
| --- | --- |
| MBIM_CID_MS_SAR_CONFIG | Windows 10 Version 1703 |
| MBIM_CID_MS_TRANSMISSION_STATUS | Windows 10 Version 1703 |

## <a name="mbim_cid_ms_sar_config"></a>MBIM_CID_MS_SAR_CONFIG

### <a name="description"></a>説明

このコマンドは、MB デバイスの SAR バックオフモードとレベルに関する情報を設定または返します。 MB デバイスは、現在の送信電力の制限を上書きし、送信アンテナに適用することで、SAR バックオフコマンドですぐに動作する必要があります。 アンテナの SAR 構成がオペレーティングシステムによって変更されていない場合は、現在の設定を維持する必要があります。 たとえば、オペレーティングシステムによってアンテナ1が SAR バックオフインデックス1に設定されている場合、アンテナ2の構成は変更せずに同じままにしておく必要があります。

このコマンドをサポートするデバイスでは、デバイス情報を OS とそのクライアントに提供するために、クエリを実装する必要があります。 Set コマンドでは、IHV と OEM の間で、各フィールドのどの値を許容できるかを定義します。 通常、SAR バックオフインデックスは、最小ベースラインとしてすべてのアンテナで構成可能であると想定されています。 デバイスでサポートされていないフィールドと共に Set 要求が送信された場合は、状態コードとして MBIM_STATUS_INVALID_PARAMETERS が返される必要があります。

各クエリまたは設定応答の後に、モデムは、モバイルブロードバンドに関連付けられているデバイス上のすべてのアンテナに関する情報を含む MBIM_MS_SAR_CONFIG 構造を返します。

#### <a name="query"></a>クエリ

MBIM_COMMAND_MSG の InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_SAR_CONFIG が返されます。

#### <a name="set"></a>オン

MBIM_COMMAND_MSG の InformationBuffer に MBIM_MS_SAR_CONFIG が含まれています。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_SAR_CONFIG が返されます。

#### <a name="unsolicited-events"></a>一方的なイベント

適用不可。

### <a name="parameters"></a>パラメーター

|  | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_SAR_CONFIG | 適用なし | 適用なし |
| Response | MBIM_MS_SAR_CONFIG | MBIM_MS_SAR_CONFIG | 利用不可 |

### <a name="data-structures"></a>データ構造

#### <a name="query"></a>クエリ

InformationBuffer は NULL にする必要があり、InformationBufferLength は0である必要があります。

#### <a name="set"></a>オン

InformationBuffer では、次の MBIM_MS_SET_SAR_CONFIG 構造体を使用する必要があります。

| Offset | サイズ | フィールド | 型 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_CONTROL_MODE | 詳細については、MBIM_MS_SAR_CONTROL_MODE の表を参照してください。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 詳細については、MBIM_MS_SAR_BACKOFF_STATE の表を参照してください。  MBIM_MS_SAR_CONTROL_MODE がデバイスで制御されるように設定されている場合、OS でこのフィールドを設定することはできません。 |
| 8 | 4 | ElementCount (EC) | UINT32 | DataBuffer で後に続く MBIM_MS_SAR_CONFIG 構造体の数。 |
| 12 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | ペアの最初の要素は4バイトオフセットで、この MBIM_MS_SET_SAR_CONFIG 構造体の先頭 (オフセット 0) から MBIM_MS_SAR_CONFIG_STATE 構造体に計算されます。 詳細については、MBIM_MS_SAR_CONFIG_STATE の表を参照してください。 ペアの2番目の要素は、対応する MBIM_MS_SAR_CONFIG_STATE 構造体へのポインターの4バイトサイズです。 |
| 12 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 構造体の配列。 |

上記の表では、次の構造が使用されています。

MBIM_MS_SAR_CONTROL_MODE は、SAR バックオフメカニズムを制御する方法を指定します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsSARControlModeDevice | 0 | SAR バックオフメカニズムは、モデムデバイスによって直接制御されます。 |
| MBIMMsSARControlModeOS | 1 | SAR バックオフメカニズムは、オペレーティングシステムによって制御および管理されます。 |

MBIM_MS_SAR_BACKOFF_STATE は、SAR バックオフの状態を示します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsSARBackOffStatusDisabled | 0 | SAR バックオフはモデムで無効になっています。 |
| MBIMMsSARBackOffStatusEnabled | 1 | モデムで SAR バックオフが有効になっています。 |

MBIM_MS_SAR_CONFIG_STATE アンテナの SAR バックオフに対して可能な状態について説明します。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARAntennaIndex | UINT32 | このテーブルの**SARBackOffIndex**フィールドに対応するアンテナインデックス。 これはアンテナ番号に対応し、デバイス上の各アンテナのインデックスを作成するために OEM の実装に残されます。 インデックスは、この値に対して有効です。 *Set*コマンドでこの値を**0xffffffff**に設定した場合は、 **SARBackOffIndex**をすべてのアンテナに適用する必要があります。 この値が " **0xffffffff** " に設定されている場合は、 **SARBackOffIndex**がすべてのアンテナに適用されていることを示します。 |
| 4 | 4 | SARBAckOffIndex | UINT32 | OEM またはモデムベンダーによって定義されたバックオフテーブルに対応するバックオフインデックス。 テーブルには、個々のバンドと関連付けられたバックオフパラメーターがあります。 |

#### <a name="response"></a>Response

InformationBuffer では、次の MBIM_MS_SAR_CONFIG 構造体を使用する必要があります。 MBIM_MS_SAR_CONFIG には、SAR の構成を指定します。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_MODE | 詳細については、MBIM_MS_SAR_CONTROL_MODE の表を参照してください。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 詳細については、MBIM_MS_SAR_BACKOFF_STATE の表を参照してください。 |
| 8 | 4 | SARWifiIntegration | MBIM_MS_SAR_ WIFI_HARDWARE_INTEGRATION | 詳細については、MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION の表を参照してください。 これは、デバイスの Wi-fi と携帯電話がハードウェアレイヤーで統合されていることを意味し、デバイスは両方の無線の SAR コントロールを自動的に調整します。 |
| 12 | 4 | ElementCount (EC) | UINT32 | DataBuffer で後に続く MBIM_MS_SAR_CONFIG_STATE 構造体の数。 |
| 16 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | ペアの最初の要素は4バイトオフセットで、この MBIM_MS_SAR_CONFIG 構造体の先頭 (オフセット 0) から MBIM_MS_SAR_CONFIG_STATE 構造体まで計算されます。 詳細については、MBIM_MS_SAR_CONFIG_STATE の表を参照してください。 ペアの2番目の要素は、対応する MBIM_MS_SAR_CONFIG_STATE 構造体へのポインターの4バイトサイズです。 |
| 16 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 構造体の配列。 |

前の表では、次の MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION 構造が使用されています。 Wi-fi と携帯ネットワークがハードウェアレベルで統合されているかどうかを指定します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsSARWifiHardwareIntegrated  | 0 | Wi-fi と携帯電話のモデム SAR は、デバイスに統合されています。 |
| MBIMMsSARWifiHardwareNotIntegrated | 1 | Wi-fi と携帯電話モデムの SAR は、デバイスには統合されていません。 |

#### <a name="notification"></a>通知

適用不可。

### <a name="status-codes"></a>状態コード

| エラー コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 要求が正常に処理されました。 |
| MBIM_STATUS_BUSY | デバイスは現在ビジー状態です。 |
| MBIM_STATUS_FAILURE | 要求が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、このコマンドをサポートしていません。 |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作に失敗しました。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作は許可されていないため、操作に失敗しました。 |

## <a name="mbim_cid_ms_transmission_status"></a>MBIM_CID_MS_TRANSMISSION_STATUS

### <a name="description"></a>説明

このコマンドは、送信状態のモデムからの通知を有効または無効にするために使用されます。 各実行プログラムが異なるチャネルの送信状態を持つことができるため、これは実行プログラムごとのコマンドです。 たとえば、デュアル SIM モデムには、LTE 上に1つ、GSM でもう一方が搭載されている場合があります。 同時に、このファイルを使用して、モデムの送信ステータスを指定することもできます。 この通知は、モデムがデータを送信しているかどうかに関係するクライアントに対して使用できます。 TX トラフィックの開始または終了が発生するたびに、モデムから通知を受け取る必要があります。 デューティサイクルが小さすぎてホストにリアルタイムで提供できない場合、状態の更新を送信する前に、ヒステリシスタイマーを使用して、設定された時間に対して TX の状態をアクティブに維持できます。 たとえば、TX が短時間バーストされ、モデムが開始通知と終了通知を時間内に提供できなかった可能性があります。 モデムは、TX トラフィックの開始時に通知を送信する必要があります。また、ヒステリシスタイマーの間に TX トラフィックを監視し続ける必要があります。 タイマーの期間内に送信された TX トラフィックがなくなった場合は、TX トラフィックが終了したことを報告する必要があります。

これは、Wi-fi と LTE の両方が接続されている場合に非常に便利です。  LTE と Wi-fi の両方が送信状態であり、近接が検出された場合は、Wi-fi バックオフが必要になることがあります。 LTE が送信中の状態ではないが、Wi-fi がの場合は、Wi-fi バックオフが必要になることがあります。 これは、一般的な Wi-fi/LTE 接続とモバイルホットスポットのシナリオに適用されます。  

Wi-fi バックオフメカニズムとコマンドは、この仕様の範囲外です。 

このコマンドを使用する Oem は、モデムが送信に関連する通知を常に送信している可能性があるため (電源の状態の削減を含む)、電源の影響を受ける可能性があることに注意する必要があります。 既定では、OS は、この通知によって最新のスタンバイ中に AP が起動され、電力パフォーマンスが向上することを許可しません。

#### <a name="query"></a>クエリ

MBIM_COMMAND_MSG の InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_TRANSMISSION_STATUS_INFO が返されます。

#### <a name="set"></a>オン

MBIM_COMMAND_MSG の InformationBuffer に MBIM_MS_SET_TRANSMISSION_STATUS が含まれています。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_TRANSMISSION_STATUS_INFO が返されます。

#### <a name="unsolicited-events"></a>一方的なイベント

未送信のイベントには MBIM_MS_TRANSMISSION_STATUS_INFO が含まれ、アクティブな無線 (OTA) チャネルに変更があったときに送信されます。 たとえば、モデムがパケットデータのアップロードを開始した場合、ネットワークデータチャネルを使用してペイロードをアップロードできるようにするには、アップリンクチャネルを設定する必要があります。 これにより、オペレーティングシステムに通知が提供されます。

### <a name="parameters"></a>パラメーター

|  | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_TRANSMISSION_STATUS | 適用なし | 適用なし |
| Response | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO |

### <a name="data-structures"></a>データ構造

#### <a name="query"></a>クエリ

MBIM_COMMAND_MSG の InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer に MBIM_MS_TRANSMISSION_STATUS_INFO が返されます。 

#### <a name="set"></a>オン

InformationBuffer では、次の MBIM_MS_SET_TRANSMISSION_STATUS 構造体を使用する必要があります。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 詳細については、MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION の表を参照してください。 |
| 4 | 4 | HysteresisTimer | UINT32 | MBIMMsTransmissionStateInactive をホストに送信するタイミングを決定するためにモデムによって使用されるヒステリシスインジケーター。 この値は、ホストにオフインジケーターを送信する前に、モデムが連続していない送信アクティビティとして認識するタイマーです。 このタイマーは、1秒から5秒の範囲で、秒単位で設定する必要があります。 |

前の表では、次の MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 構造が使用されています。 モデムチャネルの転送を無効にするか有効にするかを指定します。

| 種類 | 値 | 説明 |
| --- | --- | --- |
| MBIMMsTransmissionNotificationDisabled | 0 | モデムチャネルの送信状態通知が無効になっています。 |
| MBIMMsTransmissionNotificationEnabled | 1 | モデムチャネルの送信状態通知が有効になりました。 |

#### <a name="response"></a>Response

応答には、次の MBIM_MS_TRANSMISSION_STATUS_INFO 構造が使用されます。

| Offset | サイズ | フィールド | 型 | [説明] |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 詳細については、MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION の表を参照してください。 |
| 4 | 4 | TransmissionStatus | MBIM_MS_TRANSMISSION_STATUS | 詳細については、MBIM_MS_TRANSMISSION_STATUS の表を参照してください。 これは、5秒ごとにモデムの TX トラフィックがあるかどうかを示します。 |
| 8 | 4 | HysteresisTimer | UINT32 | MBIMMsTransmissionStateInactive をホストに送信するタイミングを決定するためにモデムによって使用されるヒステリシスインジケーター。 この値は、ホストにオフインジケーターを送信する前に、モデムが連続していない送信アクティビティとして認識するタイマーです。 このタイマーは、1秒から5秒の範囲で、秒単位で設定する必要があります。 |

前の表では、次の MBIM_MS_TRANSMISSION_STATUS 構造が使用されています。 モデムで5秒ごとに TX トラフィックが発生しているかどうかを示します。

| 種類 | 値 | [説明] |
| --- | --- | --- |
| MBIMMsTransmissionStateInactive | 0 | モデムは、最後の HysteresisTimer 値に対して継続的に伝送されることなく、データをアクティブに送信していませんでした。 |
| MBIMMsTransmissionStateActive | 1 | モデムはデータをアクティブに送信していました。 |

#### <a name="notification"></a>通知

詳細については、MBIM_MS_TRANSMISSION_STATUS_INFO の表を参照してください。

### <a name="status-codes"></a>状態コード

| エラー コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 要求が正常に処理されました。 |
| MBIM_STATUS_BUSY | デバイスは現在ビジー状態です。 | 
| MBIM_STATUS_FAILURE | 要求が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、このコマンドをサポートしていません。 |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作に失敗しました。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作は許可されていないため、操作に失敗しました。 |


