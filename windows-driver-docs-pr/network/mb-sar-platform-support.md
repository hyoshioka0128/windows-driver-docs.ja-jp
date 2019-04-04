---
title: MB SAR プラットフォームのサポート
description: MB SAR プラットフォームのサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d29378af0b76c3c3e664b75e82ad5e0c8e9313
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532525"
---
# <a name="mb-sar-platform-support"></a>MB SAR プラットフォームのサポート

## <a name="overview"></a>概要

これまでは、Oem が実装独自技術のソリューションの特定吸収レート (SAR)。 これには、OEM がユーザー モード ドライバー (UMDF) とモデムの間だけ識別されるか、またはモデムと直接対話するためのカーネル モード コンポーネントが必要ですが、デバイス サービス コマンドを実装する必要があります。 Oem もあるがありますもハイブリッド ソリューションをあるため、UMDF モデムとカーネル モード モデム コンポーネント。 ようにラジオの放射線の認識に高めましたが、モデムに sar を通過する OEM ソフトウェア コンポーネントのインターフェイスを標準化することは、次の利点について説明します。

1.  Oem は、ユーザー モード コンポーネントに向かって移動でき、ユーザー モードでのエラーがカーネル モードと比較して、システムにとって致命的でないと、システムより安定しました。
2.  Windows では、プラットフォームの標準的なインターフェイスと、Oem から独自の実装を削減できます。
3.  行政区を活用するために、プラットフォームでのサービスは、モデムから情報を取得できます。

Windows を Windows 10 バージョン 1703 以降、行政区の構成とモデムの転送状態を渡すことがサポートされています。 Windows では、自己差別化要因として使用するには、Ihv と Oem に行政区のビジネス ロジックのままに続行されますが、プラットフォームを効率化するためのインターフェイスを提供します。 このインターフェイスをサポートするために、2 つの新しい NDIS Oid と 2 つの新しい MBIM Cid が定義されています。 OS のサポートを活用するために対象のデバイスでは、両方のコマンドを実装する必要があります。

この機能は、新しい 2 つの Oid と Cid を追加してサポートされます。 MBIM を実装するための IHV パートナー、CID バージョンのみをサポートする必要があります。

> [!NOTE]
> このトピックでは、モデム デバイス ドライバーに SAR プラットフォームのサポートを実装するために、IHV パートナーのインターフェイスを定義します。 デバイスの行政区マッピング テーブルのカスタマイズに関する情報を探している場合は、[特定吸収レート (SAR) のマッピング テーブルをカスタマイズ](https://docs.microsoft.com/windows-hardware/customize/desktop/customize-sar-mapping-table)を参照してください。

## <a name="mb-interface-update-for-sar-platform-support"></a>MB インターフェイスの更新プログラム SAR プラットフォームのサポート

MBIM 準拠のデバイスでは、実装し、CID_MBIM_DEVICE_SERVICES によりクエリを実行すると、次のデバイス サービスを報告します。 既存の既知のサービスは、USB NCM MBIM 1.0 仕様のセクション 10.1 で定義されます。 Microsoft は、これを次のサービスの定義を拡張します。

サービス名 = **Microsoft SAR コントロール**

UUID = **UUID_MS_SARControl**

UUID Value = **68223D04-9F6C-4E0F-822D-28441FB72340**

| CID | 最小 OS バージョン |
| --- | --- |
| MBIM_CID_MS_SAR_CONFIG | Windows 10 Version 1703 |
| MBIM_CID_MS_TRANSMISSION_STATUS | Windows 10 Version 1703 |

## <a name="mbimcidmssarconfig"></a>MBIM_CID_MS_SAR_CONFIG

### <a name="description"></a>説明

このコマンドを設定または MB デバイスの SAR バックオフ モードとレベルに関する情報を返します。 MB デバイスは必要があります送信 power の現在の制限を上書きしたり、送信側のアンテナに適用する、すぐにコマンドのバックオフ行政区に基づいて機能します。 オペレーティング システムによってアンテナの行政区の構成を変更していない場合は、現在の設定を管理、必要があります。 たとえば、オペレーティング システムにバックオフ SAR アンテナ 1 を設定する場合インデックス 1、2 のアンテナし構成おく必要がある何も変更せず、同じ。

OS とそのクライアントにデバイス情報を提供するためにクエリを実装するには、このコマンドをサポートするデバイスと想定されます。 Set コマンドでは、各フィールドの値が許容されるかを定義するには、IHV と OEM 間です。 一般的な予測は、インデックスのバックオフ行政区、すべてのアンテナの構成可能な最小の基準としてです。 デバイスでサポートされていないフィールドのセット要求を送信する場合、状態コードとして MBIM_STATUS_INVALID_PARAMETERS を返す必要があります。

各クエリまたはセットの応答の後、モデムはモバイル ブロード バンドに関連付けられているデバイス上のすべてのアンテナの情報を含む MBIM_MS_SAR_CONFIG 構造体を返す必要があります。

#### <a name="query"></a>クエリ

MBIM_COMMAND_MSG で InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_SAR_CONFIG が返されます。

#### <a name="set"></a>設定

MBIM_COMMAND_MSG で InformationBuffer には、MBIM_MS_SAR_CONFIG が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_SAR_CONFIG が返されます。

#### <a name="unsolicited-events"></a>要請されていないイベント

適用できません。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_SAR_CONFIG | 該当なし | 該当なし |
| 応答 | MBIM_MS_SAR_CONFIG | MBIM_MS_SAR_CONFIG | 該当なし |

### <a name="data-structures"></a>データ構造体

#### <a name="query"></a>クエリ

InformationBuffer は NULL にするものとし、InformationBufferLength を 0 にする必要があります。

#### <a name="set"></a>設定

次の MBIM_MS_SET_SAR_CONFIG 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_CONTROL_MODE | 詳細については、MBIM_MS_SAR_CONTROL_MODE テーブルを参照してください。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 詳細については、MBIM_MS_SAR_BACKOFF_STATE テーブルを参照してください。  場合、デバイス制御を設定し、OS MBIM_MS_SAR_CONTROL_MODE ことは設定されませんこのフィールド。 |
| 8 | 4 | ElementCount (EC) | UINT32 | 後に、DataBuffer にカウントの MBIM_MS_SAR_CONFIG 構造体。 |
| 12 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | ペアの最初の要素は、4 バイト オフセット MBIM_MS_SAR_CONFIG_STATE 構造体をこの MBIM_MS_SET_SAR_CONFIG 構造体の先頭 (オフセット 0) から計算されます。 詳細については、MBIM_MS_SAR_CONFIG_STATE テーブルを参照してください。 ペアの 2 番目の要素は、対応する MBIM_MS_SAR_CONFIG_STATE 構造へのポインターのサイズが 4 バイトです。 |
| 12 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 構造体の配列。 |

上記の表に、次の構造が使用されます。

MBIM_MS_SAR_CONTROL_MODE は、メカニズムのバックオフ SAR を制御する方法を指定します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsSARControlModeDevice | 0 | メカニズムのバックオフ SAR が直接のモデム デバイスによって制御されます。 |
| MBIMMsSARControlModeOS | 1 | メカニズムのバックオフ SAR が制御され、オペレーティング システムによって管理されます。 |

MBIM_MS_SAR_BACKOFF_STATE では、バックオフ行政区の状態について説明します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsSARBackOffStatusDisabled | 0 | Off SAR バックアップは、モデムで無効です。 |
| MBIMMsSARBackOffStatusEnabled | 1 | Off SAR バックアップは、モデムで有効です。 |

MBIM_MS_SAR_CONFIG_STATE では、アンテナの行政区バックオフの考えられる状態について説明します。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARAntennaIndex | UINT32 | アンテナ インデックスに対応する、 **SARBackOffIndex**このテーブルのフィールド。 アンテナの番号に対応し、残りのデバイス上の各アンテナのインデックスを OEM の実装。 任意のインデックスは、この値に有効です。 この値が設定されている場合**0 xffffffff**で、*設定*コマンド、 **SARBackOffIndex**アンテナをすべてに適用する必要があります。 この値が設定されている場合**0 xffffffff**に応えて、そのことを示します**SARBackOffIndex**アンテナをすべてに適用されます。 |
| 4 | 4 | SARBAckOffIndex | UINT32 | バックオフ OEM やモデムの製造元によって定義されているテーブルに対応するインデックスのバック オフします。 テーブルには、個々 のバンドと関連するバックオフ パラメーターがあります。 |

#### <a name="response"></a>応答

次の MBIM_MS_SAR_CONFIG 構造、InformationBuffer で使用されます。 MBIM_MS_SAR_CONFIG 行政区の構成を指定します。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | SARMode | MBIM_MS_SAR_MODE | 詳細については、MBIM_MS_SAR_CONTROL_MODE テーブルを参照してください。 |
| 4 | 4 | SARBackOffStatus | MBIM_MS_SAR_BACKOFF_STATE | 詳細については、MBIM_MS_SAR_BACKOFF_STATE テーブルを参照してください。 |
| 8 | 4 | SARWifiIntegration | MBIM_MS_SAR_ WIFI_HARDWARE_INTEGRATION | 詳細については、MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION テーブルを参照してください。 これは、ハードウェア層で、デバイスの Wi-fi および移動体通信 SAR が統合されており、デバイスの両方の無線機 SAR コントロールが自動的に調整を意味します。 |
| 12 | 4 | ElementCount (EC) | UINT32 | 後に、DataBuffer にカウントの MBIM_MS_SAR_CONFIG_STATE 構造体。 |
| 16 | 8 * EC | SARConfigStatusRefList | OL_PAIR_LIST | ペアの最初の要素は 4 バイトのオフセット、MBIM_MS_SAR_CONFIG_STATE 構造体をこの MBIM_MS_SAR_CONFIG 構造体の先頭 (オフセット 0) から計算されます。 詳細については、MBIM_MS_SAR_CONFIG_STATE テーブルを参照してください。 ペアの 2 番目の要素は、対応する MBIM_MS_SAR_CONFIG_STATE 構造へのポインターの 4 つのバイト サイズです。 |
| 16 + (8 * EC) |  | DataBuffer | DATABUFFER | MBIM_MS_SAR_CONFIG_STATE 構造体の配列。 |

上記の表に、次の MBIM_MS_SAR_HARDWARE_WIFI_INTEGRATION 構造が使用されます。 これは、Wi-fi と携帯電話は、ハードウェア レベルで統合されているかどうかを指定します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsSARWifiHardwareIntegrated  | 0 | デバイスで Wi-fi と携帯電話のモデム SAR が統合されています。 |
| MBIMMsSARWifiHardwareNotIntegrated | 1 | デバイスでは、Wi-fi と携帯電話のモデム SAR が統合されていません。 |

#### <a name="notification"></a>通知

適用できません。

### <a name="status-codes"></a>状態コード

| エラー コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 要求が正常に処理します。 |
| MBIM_STATUS_BUSY | デバイスは現在ビジー状態です。 |
| MBIM_STATUS_FAILURE | 要求が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスでは、このコマンドはサポートしません。 |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作が失敗しました。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作が許可されていないため、操作が失敗しました。 |

## <a name="mbimcidmstransmissionstatus"></a>MBIM_CID_MS_TRANSMISSION_STATUS

### <a name="description"></a>説明

このコマンドを有効または無効、モデムからの通知に使用で状態を送信します。 各 executor は、さまざまなチャネルの転送状態を持つことができます、executor あたりのコマンドになります。 たとえば、デュアル SIM モデム LTE と、その他のいずれかにあります GSM。 同時に、モデムの送信の状態を提供する使用できます。 この通知は、かどうか、モデムがデータを送信かどうかに関心のあるクライアントに対して使用できます。 モデムは、開始または送信トラフィックの末尾にあるいつ通知を提供します。 デューティ サイクルが小さすぎると、ホストにリアルタイムで提供することはできない場合、TX 状態に対して保持できるアクティブとして設定した時刻ヒステリシス タイマーを使用した状態の更新を送信する前にします。 たとえば、テキサス州の短くバーストが発生しましたし、モデムが時間の開始と終了の通知を提供できなかったことがあります。 モデムは、送信トラフィックの開始時に通知を送信する必要がありますヒステリシス タイマーの中に、送信トラフィックを監視を続行する必要があります。 送信トラフィックは、タイマーの時間枠内で生成された場合、レポート送信トラフィックが終了したことです。

これは、Wi-fi と LTE の両方が接続されているシナリオで非常に役立ちます。  LTE と Wi-fi の両方が送信状態近接が検出された場合、Wi-fi 戻る off 必要があります。 LTE が状態の送信にはありませんが、Wi-fi が、Wi-fi のバックオフし、場合は、必要なできない可能性があります。 これは、一般的な Wi-Fi/LTE 接続とモバイル ホット スポットのシナリオに適用されます。  

Wi-fi バックオフ メカニズムとコマンドは、この仕様の範囲外です。 

このコマンドを使用する Oem power 影響対応モデムは、常に制限の電源状態を含む転送に関連する通知を送信する可能性があります。 OS、既定ではできません電源のパフォーマンスを向上させるために最新のスタンバイ中に、AP を起動するには、この通知。

#### <a name="query"></a>クエリ

MBIM_COMMAND_MSG で InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_SET_TRANSMISSION_STATUS_INFO が返されます。

#### <a name="set"></a>設定

MBIM_COMMAND_MSG で InformationBuffer には MBIM_MS_SET_TRANSMISSION_STATUS が含まれています。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_SET_TRANSIMISSION_STATUS の機能はありませんが返されます。

#### <a name="unsolicited-events"></a>要請されていないイベント

要請されていないイベントは、MBIM_MS_TRANSMISSION_STATUS_INFO を含み、アクティブな無線 (OTA) チャンネルに変更があるときに送信されます。 たとえば、モデムには、パケット データのアップロードが開始されている場合、ペイロードをアップロードできるように、ネットワークのデータ チャネルを使用する場合に、アップリンク チャネルを設定する必要があります。 これにより、オペレーティング システムに提供される通知がトリガーされます。

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | MBIM_MS_SET_TRANSMISSION_STATUS | 該当なし | 該当なし |
| 応答 | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO | MBIM_MS_TRANSMISSION_STATUS_INFO |

### <a name="data-structures"></a>データ構造体

#### <a name="query"></a>クエリ

MBIM_COMMAND_MSG で InformationBuffer は使用されません。 MBIM_COMMAND_DONE の InformationBuffer MBIM_MS_TRANSMISSION_STATUS_INFO が返されます。 

#### <a name="set"></a>設定

次の MBIM_MS_SET_TRANSMISSION_STATUS 構造、InformationBuffer で使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 詳細については、MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION テーブルを参照してください。 |
| 4 | 4 | HysteresisTimer | UINT32 | ホストに、MBIMMsTransmissionStateInactive を送信するときに、モデムで使用されるヒステリシス インジケーター。 この値は、タイマーのように、継続的ないいえ-送信アクティビティ OFF インジケーターをホストに送信する前に、モデムが表示されます。 このタイマーは、1 秒から 5 秒間に至るまでの秒単位で設定する必要があります。 |

上記の表に、次の MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION 構造が使用されます。 これは、モデムのチャネルの転送が無効または有効になっているかどうかを指定します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsTransmissionNotificationDisabled | 0 | モデム チャネル転送状態通知が無効になっています。 |
| MBIMMsTransmissionNotificationEnabled | 1 | モデム チャネル転送状態通知が有効にします。 |

#### <a name="response"></a>応答

次の MBIM_MS_TRANSMISSION_STATUS_INFO 構造は、応答に使用されます。

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | ChannelNotification | MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION | 詳細については、MBIM_MS_TRANSMISSION_STATUS_NOTIFICATION テーブルを参照してください。 |
| 4 | 4 | TransmissionStatus | MBIM_MS_TRANSMISSION_STATUS | 詳細については、MBIM_MS_TRANSMISSION_STATUS テーブルを参照してください。 これかどうかをモデム TX トラフィック 5 秒ごとです。 |
| 8 | 4 | HysteresisTimer | UINT32 | ホストに、MBIMMsTransmissionStateInactive を送信するときに、モデムで使用されるヒステリシス インジケーター。 この値は、タイマーのように、継続的ないいえ-送信アクティビティ OFF インジケーターをホストに送信する前に、モデムが表示されます。 このタイマーは、1 秒から 5 秒間に至るまでの秒単位で設定する必要があります。 |

上記の表に、次の MBIM_MS_TRANSMISSION_STATUS 構造が使用されます。 かどうかモデムがある送信トラフィック 5 秒ごとを示します。

| 種類 | Value | 説明 |
| --- | --- | --- |
| MBIMMsTransmissionStateInactive | 0 | モデムがないデータを転送 HysteresisTimer の最後の値の転送の継続的な遅延なし。 |
| MBIMMsTransmissionStateActive | 1 | モデムでは、データを転送がアクティブにします。 |

#### <a name="notification"></a>通知

詳細については、MBIM_MS_SET_TRANSMISSION_STATUS_INFO テーブルを参照してください。

### <a name="status-codes"></a>状態コード

| エラー コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 要求が正常に処理します。 |
| MBIM_STATUS_BUSY | デバイスは現在ビジー状態です。 | 
| MBIM_STATUS_FAILURE | 要求が失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスでは、このコマンドはサポートしません。 |
| MBIM_STATUS_INVALID_PARAMETERS | 無効なパラメーターのため、操作が失敗しました。 |
| MBIM_STATUS_OPERATION_NOT_ALLOWED | 操作が許可されていないため、操作が失敗しました。 |


