---
title: MB NITZ サポート
description: MB NITZ サポート
ms.assetid: 94FE0380-C5EA-49F7-A649-0524C27F1A35
keywords:
- MB NITZ サポート、モバイルブロードバンド NITZ サポート
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9dd754e5dd15d2af8739d7c54957fdd5adbe8507
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557733"
---
# <a name="mb-nitz-support"></a>MB NITZ サポート

## <a name="overview"></a>概要

Windows 10 バージョン1903以降では、Windows は、モバイルブロードバンド (MBB) デバイスの OS レベルでのネットワーク Id とタイムゾーン (NITZ) をサポートしています。 以前のバージョンの Windows では、3GPP に準拠しているすべてのモデムによってモデムレベルで NITZ がサポートされていた場合でも、OS レベルで使用できる唯一のネットワーク時間はネットワークタイムプロトコル (NTP) でした。 NITZ のサポートにより、Windows はモデムから要請されていない NITZ 通知を受信し、必要なイベントを発行して NITZ タイムスタンプのコンシューマーに通知することができます。

MBIM 関数の場合、追加の NITZ 関連のセットアップとプロビジョニングは必要ありません。 携帯ネットワークのベアラー経由でデータ接続が確立されている限り、モデムは、ネットワークから NITZ タイムスタンプを受け取ったときにいつでも OS に通知できます。 モデムは、3GPP 仕様内で、携帯事業者独自に定義したリズムとスケジュールに基づいて、ネットワークインフラストラクチャから NITZ 通知を受け取ることができます。 NITZ 通知は要求されません。 NITZ の通知を受信すると、OS は NITZ データが使用可能であるという通知を発行します。

## <a name="ndis-interface-extension"></a>NDIS インターフェイス拡張

次の OID は、NITZ をサポートするように定義されています。

- [OID_WWAN_NITZ](oid-wwan-nitz.md)

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| [サービス名] | UUID | UUID の値 |
| --- | --- | --- |
| Microsoft 基本 IP 接続拡張機能 | UUID_VOICEEXTENSIONS | 8d8b9eba-37be-449b-8f1e-61cb034a702e |

次の表では、各 CID の UUID とコマンドコードに加えて、CID が Set、Query、または Event (通知) 要求をサポートしているかどうかを示します。 パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個別のセクションを参照してください。 

| CID | UUID | コマンドコード | オン | クエリ | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_NITZ | UUID_VOICEEXTENSIONS | 10 | N | Y | Y |

## <a name="mbim_cid_nitz"></a>MBIM_CID_NITZ

### <a name="parameters"></a>パラメーター

| 操作 | オン | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 適用なし | 適用なし | 適用なし |
| 応答 | 適用なし | MBIM_NITZ_INFO | MBIM_NITZ_INFO |

### <a name="query"></a>クエリ

現在のネットワーク時間を照会します。 MBIM_COMMAND_MSG の InformationBuffer は使用されません。 次の MBIM_NITZ_INFO 構造は、MBIM_COMMAND_DONE の InformationBuffer で使用されます。

#### <a name="mbim_nitz_info"></a>MBIM_NITZ_INFO

| Offset | サイズ | フィールド | Type | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 年 | UINT32 | 整数としての年。 たとえば、 **2014**のようになります。 |
| 4 | 4 | 月 | UINT32 | 月 (1 ~ 12)。1月 = = 1 です。 |
| 8 | 4 | 日 | UINT32 | 月の日にち (1 ~ 31)。 |
| 12 | 4 | Hour | UINT32 | 時間 (0 ~ 23)。 |
| 16 | 4 | 分 | UINT32 | 分、(0 ~ 59)。 |
| 20 | 4 | Second | UINT32 | 2番目の (0 ~ 59)。 |
| 24 | 4 | TimeZoneOffsetMinutes | UINT32 | UTC からのタイムゾーンオフセット (分単位)。 この値には、夏時間の現在の状態に対する調整が含まれます。 タイムゾーン情報を使用できない場合は、この値を0xFFFFFFFF に設定する必要があります。 |
| 28 | 4 | DaylightSavingTimeOffsetMinutes | UINT32 | 夏時間のオフセット (分単位)。 夏時間を使用できない場合は、この値を0xFFFFFFFF に設定する必要があります。 |
| 32 | 4 | Dataclasses.dll | UINT32 | このネットワークでサポートされるデータクラス。 この情報が利用できない場合は、このフィールドを MBIMDataClassNone に設定する必要があります。 |

### <a name="set"></a>オン

適用不可。

### <a name="response"></a>応答

MBIM_COMMAND_DONE の InformationBuffer に MBIM_NITZ_INFO 構造体が含まれています。

### <a name="unsolicited-events"></a>一方的なイベント

この要請されていないイベントは、現在のネットワーク時刻とタイムゾーンの情報を提供します。

### <a name="status-codes"></a>状態コード

この CID は、 [Mbim 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)のセクション9.4.5 で定義されている汎用ステータスコードのみを使用します。
