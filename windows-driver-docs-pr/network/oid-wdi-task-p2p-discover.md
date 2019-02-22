---
title: OID_WDI_TASK_P2P_DISCOVER
description: OID_WDI_TASK_P2P_DISCOVER は、Wi-Fi Direct の検出を実行するデバイスに発行されます。
ms.assetid: 9425a8d1-af68-488c-8a1e-a9b759f102cc
ms.date: 07/18/2017
keywords:
- OID_WDI_TASK_P2P_DISCOVER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 8807d5952e61b438093d1a0df0c1a12cd5bbba9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551108"
---
# <a name="oidwditaskp2pdiscover"></a>OID\_WDI\_タスク\_P2P\_検出


OID\_WDI\_タスク\_P2P\_検出が Wi-Fi Direct の検出を実行するデバイスに発行します。

| オブジェクト | 中止できます。                                           | 既定の優先順位 (ホスト ドライバー ポリシー) | 通常の実行時間 (秒) |
|--------|---------------------------------------------------------|---------------------------------------|---------------------------------|
| ポート   | [はい]。 ポートは、中止した後、クリーンな状態でなければなりません。 | 6                                     | 15                              |

 

コマンドには、特定のセット検索して、Wi-Fi Direct デバイスまたはワイルドカード検出のにはいずれかを定義するプロパティが含まれています。

Wi-Fi Direct の検出は、標準的な Wi-fi スキャンの対象から相互に排他的です。 このタスクを実行すると、中に「直接の」SSID、または特定の移動の SSID せずブロードキャスト プローブ要求は送信されません。 これらのプローブ要求には、すべての必要な Wi-Fi Direct IEs おく必要があります。

ホストがデバイスにタスクのパラメーターの一部として指定されていない検索条件があります。 必須の条件に一致することが場合、ホストがタスクの中止メカニズムを使用して可能性があります、そのため、デバイスが Wi-Fi Direct 検出タスクをすばやく中止できることが重要がシナリオのパフォーマンスが低下することにならないようにします。

(通常または中止のため)、タスクが完了したら、ときに、そのポートで別の検出要求を発行できるように、ポートが正常な状態でなければなりません。

## <a name="task-parameters"></a>タスク パラメーター


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>許可されている複数の TLV インスタンス</th>
<th>省略可能</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897878" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_DISCOVER_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897878)"><strong>WDI_TLV_P2P_DISCOVER_MODE</strong></a></td>
<td></td>
<td></td>
<td>スキャンの種類、数、およびスキャンの間隔などの検出モード情報。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898051" data-raw-source="[&lt;strong&gt;WDI_TLV_SCAN_DWELL_TIME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898051)"><strong>WDI_TLV_SCAN_DWELL_TIME</strong></a></td>
<td></td>
<td></td>
<td>ドウェル時刻の設定をスキャンしています。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897877" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_DISCOVERY _CHANNEL_SETTINGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897877)"><strong>WDI_TLV_P2P_DISCOVERY _CHANNEL_SETTINGS</strong></a></td>
<td>X</td>
<td>X</td>
<td>期間とをスキャンするチャネルの一覧をスキャンします。 指定した場合、リッスンの設定をオーバーライド WDI_TLV_SCAN_DWELL_TIME で指定されています。 このリストが空の場合、ポートがでサポートされているすべてのチャンネル スキャンし、WDI_TLV_SCAN_DWELL_TIME からリッスン設定を使用する必要があります。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898064" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898064)"><strong>WDI_TLV_SSID</strong></a></td>
<td>X</td>
<td>X</td>
<td>ポートをスキャンする必要がある Ssid の一覧。 この一覧で複数の Ssid 許可されるは、ワイルドカードは、それらのいずれか。 チャネルで作業中のスキャンを実施する際に、ポートは、一覧には、各 SSID のプローブ要求を送信する必要があります。 このリストが空の場合は、Ssid のすべてのポートをスキャンする必要があります。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898009" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_NAME_HASH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898009)"><strong>WDI_TLV_P2P_SERVICE_NAME_HASH</strong></a></td>
<td>X</td>
<td>X</td>
<td>クエリを実行するハッシュのサービス名の一覧。 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY または WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY が指定されているかどうかに必要です。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898076" data-raw-source="[&lt;strong&gt;WDI_TLV_VENDOR_SPECIFIC_IE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898076)"><strong>WDI_TLV_VENDOR_SPECIFIC_IE</strong></a></td>
<td></td>
<td>X</td>
<td>ポートによって送信されたプローブ要求に含める必要がある 1 つまたは複数の i。 これらでは、パッシブ スキャンは使用されません。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt269140" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt269140)"><strong>WDI_TLV_P2P_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></td>
<td>X</td>
<td>X</td>
<td>クエリを実行するサービス情報の検出のエントリのオプションのリスト。 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_INFORMATION が指定されている場合、この機能が必要です。 サービス名のハッシュを使用してプローブ要求/応答に対して P2P サービスの検出を実行するには、ドライバーが必要です。 サービス情報を含むサービス エントリごとに、ドライバーは、実行、ANQP クエリ要求/応答サービスの情報を照会すると想定されます。</td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769912" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769912)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p></td>
<td>X</td>
<td><p>X</p></td>
<td><p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p>
<p>クエリを実行する ASP2 サービス情報の検出のエントリのオプションのリスト。 WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION が指定されている場合、この機能が必要です。 サービス名のハッシュを使用してプローブ要求/応答に対して P2P サービスの検出を実行するには、ドライバーが必要です。 サービス情報を含むサービス エントリごとに、ドライバーは、実行、ANQP クエリ要求/応答サービスの情報を照会すると想定されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769913" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769913)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p></td>
<td></td>
<td><p>X</p></td>
<td><p>Windows 10 version 1607 では、バージョン 1.0.21 WDI に追加されます。</p>
<p>プローブ要求が探索時にリッスンのチャネルの属性を含めるかどうかを指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>タスクの完了を示す値


[NDIS\_状態\_WDI\_INDICATION\_P2P\_検出\_完了](ndis-status-wdi-indication-p2p-discovery-complete.md)
## <a name="unsolicited-indication"></a>要請されていないを示す値


[NDIS\_状態\_WDI\_INDICATION\_BSS\_エントリ\_一覧](ndis-status-wdi-indication-bss-entry-list.md)要件
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

 

 




