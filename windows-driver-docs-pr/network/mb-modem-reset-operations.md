---
title: MB モデム リセット操作
description: MB モデム リセット操作
ms.assetid: E33073B5-53D5-4F6F-85EC-5B46FDE9EA4D
keywords:
- MB モデムのリセット、モバイル ブロード バンド モデムをリセットするミニポート ドライバーのモバイル ブロード バンド モデムのリセット
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6172d1949ae8b52a8c353f26503d14ad01435a80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343289"
---
# <a name="mb-modem-reset-operations"></a>MB モデム リセット操作

このセクションでは、MBIM CID コマンドとデータ構造体だけでなく NDIS OID コマンドとモバイル ブロード バンド (MB) デバイスでモデムをリセットするためのデータ構造を定義します。 これらのコマンドとデータ構造体、Windows 10 バージョン 1709 以降で利用できます。

## <a name="mbimcidmsdevicereset"></a>MBIM_CID_MS_DEVICE_RESET

ホストは、モデム デバイスをリセットする MBIM 関数に MBIM_CID_MS_DEVICE_RESET を送信します。

| サービス名 | UUID | UUID 値 |
| --- | --- | --- |
| Microsoft Basic IP 接続の拡張機能 | UUID_BASIC_CONNECT_EXTENSIONS | 3d01dcc5-fef5-4d05-0d3a-bef7058e9aaf |

| CID | コマンド コード | 設定 | クエリ | 通知 |
| --- | --- | --- | --- | --- |
| MBIM_CID_MS_DEVICE_RESET | 10 | Y | N | N |

### <a name="parameters"></a>パラメーター

|   | 設定 | クエリ | 通知 |
| --- | --- | --- | --- |
| コマンド | 空 | 該当なし | 該当なし |
| 応答 | 空 | 該当なし | 該当なし |

### <a name="query"></a>クエリ

適用できません。

### <a name="set"></a>Set

NULL にする必要があります、InformationBuffer と*InformationBufferLength* 0 にする必要があります。

### <a name="response"></a>応答

NULL にする必要があります、InformationBuffer と*InformationBufferLength* 0 にする必要があります。

### <a name="notification"></a>通知

適用できません。

### <a name="status-codes"></a>状態コード

次のステータス コードが適用されます。 状態は、リセットが完了したら、設定操作に非同期の応答として返されます。

| 状態コード | 説明 |
| --- | --- |
| MBIM_STATUS_SUCCESS | 操作に成功しました。 |
| MBIM_STATUS_BUSY | デバイスがビジーです。 |
| MBIM_STATUS_FAILURE | 操作に失敗しました。 |
| MBIM_STATUS_NO_DEVICE_SUPPORT | デバイスは、この操作をサポートしていません。 |

## <a name="oidwwandevicereset"></a>OID_WWAN_DEVICE_RESET

MBIM_CID_MS_DEVICE_RESET の NDIS 相当するものは[OID_WWAN_DEVICE_RESET](oid-wwan-device-reset.md)します。
