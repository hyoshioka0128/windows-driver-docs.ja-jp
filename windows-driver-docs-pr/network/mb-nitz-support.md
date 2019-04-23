---
title: MB NITZ サポート
description: MB NITZ サポート
ms.assetid: 94FE0380-C5EA-49F7-A649-0524C27F1A35
keywords:
- MB NITZ サポート、モバイル ブロード バンド NITZ サポート
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 09cfce70987bd3e19955449250dc88b793a1c7a2
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905449"
---
# <a name="mb-nitz-support"></a>MB NITZ サポート

## <a name="overview"></a>概要

Windows 10、バージョンが 1903 年以降 Windows ネットワーク Id とタイム ゾーン (NITZ)、OS レベルでデバイスのサポート モバイル ブロード バンド (MBB)。 Windows の以前のバージョンでは、OS レベルで利用可能な唯一のネットワーク時間は、NITZ が 3 gpp 準拠のすべてのモデムでモデム レベルでサポートされている場合でもネットワーク タイム プロトコル (NTP) をしました。 NITZ サポートでは、Windows はモデムから要請されていない NITZ 通知を受信し、NITZ タイムスタンプのコンシューマーに通知するために必要なイベントを発行できます。

MBIM 関数では、追加のありません NITZ 関連の設定とプロビジョニングが必要です。 モデムを携帯電話のベアラー経由でデータ接続が確立されると、としては、OS が NITZ タイムスタンプ、ネットワークから受信したすべての時間に通知できます。 モデムは、携帯電話会社独自の定義されたパターンと、3 gpp 仕様内でのスケジュールに基づくネットワーク インフラストラクチャから NITZ 通知を受信できます。 NITZ 通知が要請されたではありません。 NITZ 通知を受信すると、OS は NITZ データが使用可能な通知を発行します。

## <a name="ndis-interface-extension"></a>NDIS インターフェイスの拡張機能

次の OID は NITZ をサポートするために定義されています。

- [OID_WWAN_NITZ](oid-wwan-nitz.md)

## <a name="mbim-service-and-cid-values"></a>MBIM サービスと CID 値

| サービス名 | UUID | UUID 値 |
| --- | --- | --- |
| Microsoft Basic IP 接続の拡張機能 | UUID_VOICEEXTENSIONS | 8d8b9eba-37be-449b-8f1e-61cb034a702e |

次の表に、UUID を指定して、各 CID のコードをコマンドだけでなく、CID がサポートしているかどうかを設定、クエリ、またはイベント (通知) を要求します。 詳細については、パラメーター、データ構造、および通知の詳細については、このトピック内の各 CID の個々 のセクションを参照してください。 

| CID | UUID | コマンド コード | 設定 | クエリ | 通知 |
| --- | --- | --- | --- | --- | --- |
| MBIM_CID_NITZ | UUID_VOICEEXTENSIONS | 10 | N | Y | Y |

## <a name="mbimcidnitz"></a>MBIM_CID_NITZ

### <a name="parameters"></a>パラメーター

|  | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 該当なし | 適用なし | 該当なし |
| 応答 | 該当なし | MBIM_NITZ_INFO | MBIM_NITZ_INFO |

### <a name="query"></a>クエリ

現在のネットワークの時間を照会します。 MBIM_COMMAND_MSG の InformationBuffer は使用されません。 次の MBIM_NITZ_INFO 構造は、MBIM_COMMAND_DONE InformationBuffer に使用されます。

#### <a name="mbimnitzinfo"></a>MBIM_NITZ_INFO

| Offset | サイズ | フィールド | 種類 | 説明 |
| --- | --- | --- | --- | --- |
| 0 | 4 | 年 | UINT32 | 年の整数。 たとえば、 **2014**します。 |
| 4 | 4 | Month | UINT32 | (1..12)、月、年 1 月 = 1 を = です。 |
| 8 | 4 | 日 | UINT32 | (1..31)、月の日にち。 |
| 12 | 4 | Hour | UINT32 | 時間、(0..23)。 |
| 16 | 4 | Minute | UINT32 | 分、(0..59)。 |
| 20 | 4 | 第 2 週 | UINT32 | 秒、(0..59)。 |
| 24 | 4 | TimeZoneOffsetMinutes | UINT32 | UTC からの分単位でのタイム ゾーン オフセット。 この値には、夏時間の現在の状態の調整が含まれています。 タイム ゾーン情報が利用できない場合、この値を 0 xffffffff に設定する必要があります。 |
| 28 | 4 | DaylightSavingTimeOffsetMinutes | UINT32 | 夏時間の分単位のオフセット。 夏時間が利用できない場合、この値を 0 xffffffff に設定する必要があります。 |
| 32 | 4 | DataClasses | UINT32 | このネットワークでサポートされているデータ クラスです。 この情報が利用できない場合、このフィールドは MBIMDataClassNone に設定する必要があります。 |

### <a name="set"></a>Set

適用できません。

### <a name="response"></a>応答

MBIM_COMMAND_DONE で InformationBuffer には MBIM_NITZ_INFO 構造体が含まれています。

### <a name="unsolicited-events"></a>要請されていないイベント

要請されていないこのイベントは、現在のネットワーク時刻とタイム ゾーン情報を提供します。

### <a name="status-codes"></a>状態コード

この CID がのみの 9.4. 5. のセクションで定義された汎用的なステータス コードを使用して、 [MBIM 仕様リビジョン 1.0](https://www.usb.org/sites/default/files/MBIM10Errata1_073013.zip)します。
