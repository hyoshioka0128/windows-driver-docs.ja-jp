---
title: OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY
description: OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY がバック グラウンドで定期的に Wi-Fi Direct の検出を実行するアダプターを指示します
ms.assetid: DF58B71D-7D45-4E0D-963F-A70471363DF5
ms.date: 07/18/2017
keywords:
- OID_WDI_SET_P2P_START_BACKGROUND_DISCOVERY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: a62c2b90748b8903c21024851e89b68061e51b5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359185"
---
# <a name="oidwdisetp2pstartbackgrounddiscovery"></a>OID\_WDI\_設定\_P2P\_開始\_バック グラウンド\_検出


OID\_WDI\_設定\_P2P\_開始\_バック グラウンド\_検出が定期的に、バック グラウンドで Wi-Fi Direct の検出を実行するアダプターを指示します

| Scope | タスクでシリアル化された設定します。 | 通常の実行時間 (秒) | データのスループットと待機時間を影響します。 |
|-------|--------------------------|---------------------------------|---------------------------------|
| ポート  | X                       | 1                               | 〇                             |

 

アダプターは、一定の間隔で指定されたチャネルをスキャンし、デバイスの表示タイムアウト (通常は 5 分) 内で検出可能になるデバイスを検索できるに必要です。 動作は通常の Wi-Fi Direct 検出スキャンに似ています (で定義されている[OID\_WDI\_タスク\_P2P\_DISCOVER](oid-wdi-task-p2p-discover.md)) が、期限付きでないし、アダプターがスケジュールを設定時間の後である時点でスキャンします。 アダプターは、各デバイスの可視性のタイムアウト時間内に少なくとも 1 つのスキャンを実行する必要があります。 デバイスの表示タイムアウトが 0 の場合、アダプターは定期的に、独自のサイクル タイムを使用してスキャンする続行する必要があります。 スキャン、またはタスクの要求がこの期間中に行われた場合、アダプターはタスクの実行中のバック グラウンドの検出を中断し、タスクの完了時に続行する必要があります。 バック グラウンドのスキャンを完了すると、デバイスを送信する必要があります、 [NDIS\_状態\_WDI\_INDICATION\_P2P\_検出\_完了](ndis-status-wdi-indication-p2p-discovery-complete.md)表記 (トランザクション ID は 0) に、オペレーティング システムにスキャンが完了したことを通知できるようにします。 アダプターは、バック グラウンドのスキャンが完了するたびに、このを示す値を送信する必要があります。

チャネルの一覧が指定されている場合のみ指定されたチャネルでアダプターをスキャンする必要があります。 それ以外の場合、すべてのチャネルでスキャンする必要があります。 指定したチャネルの外部でデバイスを検出するファームウェアが発生した場合情報をオペレーティング システムに送信する必要があります。

期間とチャネルをリッスンすると ([**WDI\_TLV\_P2P\_検出\_チャネル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-discovery-channel-settings)) が指定すると、参照します。リモート デバイスの待機時間。 アダプターは、待機時間とチャネルのすべての値に基づいて最も効率的な方法で要求されたチャネルをスキャンするスケジュールを考案する必要があります。 オペレーティング システムでは、待機時間とチャンネルの複数のインスタンスを指定できますも。 この場合、アダプターする必要がありますまずを思い付くリッスン期間とチャネルのリストの 0 以外の値を持つこれらのエントリのスキャンのスケジュール。 次に、アダプターでは、次の場合に既定値を使用する必要があります。

1.  待機期間が 0 の場合、アダプターは、指定したチャネルの既定のスキャン時間を使用してください。
2.  チャネルの一覧が空の場合、アダプターはそのバンドの指定されたリッスンとサイクルの時間を使用してそのバンド内のチャネルのすべてをスキャンする必要があります。 時間は適用されませんを持つ独立した任意のチャンネル スキャンでは、オペレーティング システムで指定された期間をリッスンします。

アダプターとして特定のサービス名に対するプローブ要求に応答を示します、NIC が D0、 [NDIS\_状態\_WDI\_INDICATION\_BSS\_エントリ\_一覧](ndis-status-wdi-indication-bss-entry-list.md)オペレーティング システムに通知します。 WDI は、上位層サービスは、OS の応答情報をキャッシュし、必要なことが通知されます。

D2 の NIC がある場合は、D0 に戻るまで、バック グラウンドの検出を中断します。

## <a name="set-property-parameters"></a>プロパティ パラメーターの設定


| TLV                                                                                                | 許可されている複数の TLV インスタンス | 省略可能 | 説明                                                                                                                         |
|----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_バック グラウンド\_DISCOVER\_モード**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-background-discover-mode)     |                                |          | Wi-Fi Direct バック グラウンドの検出モード パラメーター。                                                                                   |
| [**WDI\_TLV\_P2P\_検出\_チャネル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-discovery-channel-settings) | x                              | x        | 一覧は、スキャンするチャネルをお勧めします。                                                                                               |
| [**WDI\_TLV\_P2P\_DEVICE\_FILTER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-device-filter-list)                 |                                | x        | Wi-Fi Direct デバイスとデバイスの Wi-Fi Direct 時に検索するグループの所有者の一覧を検出します。                                    |
| [**WDI\_TLV\_P2P\_サービス\_名前\_ハッシュ**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-name-hash)                   | x                              | x        | クエリを実行するハッシュのサービス名のリスト。 これは、必要な場合 WDI\_P2P\_サービス\_検出\_型\_サービス\_名前\_のみを指定します。 |
| [**WDI\_TLV\_ベンダー\_特定\_IE**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-vendor-specific-ie)                          |                                | x        | ポートによって送信されたプローブ要求に含める必要がある 1 つまたは複数の i。                                                       |

 

## <a name="set-property-results"></a>セットのプロパティの結果


追加データがありません。 ヘッダー内のデータで十分です。
## <a name="unsolicited-indication"></a>要請されていないを示す値


[NDIS\_STATUS\_WDI\_INDICATION\_BSS\_ENTRY\_LIST](ndis-status-wdi-indication-bss-entry-list.md)

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




