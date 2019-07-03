---
title: バグ チェック 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
description: BUGCODE_NDIS_DRIVER_LIVE_DUMP バグのコードでは、0x0000015E の値を持ちます。 このバグのコードでは、NDIS がライブ カーネル ダンプをキャプチャしたことを示します。 NDIS には、このような状況でのバグ チェックが生成されません。
ms.assetid: 3663A955-A1D7-4880-BD83-0976012F2CB1
keywords:
- バグ チェック 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
- BUGCODE_NDIS_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_NDIS_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 844d65b5cc033dc6b03ba4028078461f774dbf1e
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520000"
---
# <a name="bug-check-0x15e-bugcodendisdriverlivedump"></a>バグ チェック 0x15E:BUGCODE\_NDIS\_ドライバー\_LIVE\_ダンプ


BUGCODE\_NDIS\_ドライバー\_LIVE\_ダンプ バグ コードが 0x0000015E の値を持ちます。 このバグのコードでは、NDIS がライブ カーネル ダンプをキャプチャしたことを示します。 NDIS には、このような状況でのバグ チェックが生成されません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="bugcodendisdriver-parameters"></a>BUGCODE\_NDIS\_ドライバーのパラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。 つまり、パラメーターの値が「0」の場合はは使用されません。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメーター 1 の値とエラーの原因</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FATAL_ERROR</p>
<p>ミニポート ドライバーでは、致命的なエラーが発生し、再列挙を要求します。</p></td>
<td align="left"><p>ミニポート ブロックのアドレス。 実行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd.minidriver</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>ミニポートの物理デバイス オブジェクト (PDO) のアドレス</p></td>
<td align="left"><p>このライブ ダンプされる原因となった致命的なエラーです。 設定可能な値:</p>
<ol>
<li>70:ユーザー モードに起因</li>
<li>71:による <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismremoveminiport" data-raw-source="[NdisMRemoveMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismremoveminiport)">NdisMRemoveMiniport</a></strong></li>
<li>72:による<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex" data-raw-source="[NdisIMInitializeDeviceInstanceEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)">NdisIMInitializeDeviceInstanceEx</a></strong>失敗</li>
<li>73:による<em><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart" data-raw-source="[MiniportRestart](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)">MiniportRestart</a></em>失敗</li>
<li>74:失敗の原因となった、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER (D0)](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER (D0)</a>要求</li>
<li>75:失敗の原因となった、 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER (Dx)](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER (Dx)</a>要求</li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>ネットワーク スタックを管理しようとすると、時間がかかりすぎています。 NDIS は、他のドライバーに呼び出す、NDIS は呼び出しが迅速に完了したことを確認するウォッチドッグ タイマーを開始します。 呼び出し時間がかかりすぎる場合、NDIS はバグチェックを挿入します。</p>
<p>単純なデッドロックの可能性があります。 検索"! スタックの 2 つの ndis"または類似したにすべてのスレッド検索疑わしいかどうかを参照してください。 NDIS_WATCHDOG_TRIAGE_BLOCK、PrimaryThread に特別な注意してください。</p>
<p>可能性がありますが失われた NBLs、後者<strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">! ndiskd.pendingnbls</a></strong>役立つ場合があります。 チェックを使用して保持されている Oid を <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! ndiskd.oid</a></strong>します。</p></td>
<td align="left"><p>この操作は、時間がかかりすぎました。 設定可能な値:</p>
<ul>
<li><p>0x01 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>プロトコル ドライバーを一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x02 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>NET_PNP_EVENT_NOTIFICATION をプロトコル ドライバーに配信中にタイムアウトが発生しました。</p></li>
<li><p>0x03 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>状態の表示をプロトコル ドライバーに配信中にタイムアウトが発生しました。</p></li>
<li><p>0x04 :NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>プロトコル ドライバーをバインド解除中にタイムアウトが発生しました。</p></li>
<li><p>パターン:NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>フィルター ドライバーを一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x12:NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>フィルター ドライバー、NET_PNP_EVENT_NOTIFICATION を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x13:NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>フィルター ドライバーの状態を示す値を提供する一方、タイムアウトが発生しました。</p></li>
<li><p>0x14:NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>フィルター ドライバーのデタッチ中にタイムアウトが発生しました。</p></li>
<li><p>0x21:NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>ミニポート アダプタを一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x22:NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>ミニポート アダプターが停止中にタイムアウトが発生しました。</p></li>
<li><p>0x23:NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>ミニポート アダプターに、OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x24:NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>フィルター ドライバー、OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x25:NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>ミニポート アダプターをアイドル状態である中にタイムアウトが発生しました。</p></li>
<li><p>0x26:NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>ミニポート アダプターをアイドル状態の要求のキャンセル中にタイムアウトが発生しました。</p></li>
</ul></td>
<td align="left"><p>Ndis にキャストされます。NDIS_WATCHDOG_TRIAGE_BLOCK します。 有用なフィールド:</p>
<ul>
<li><strong>StartTime</strong> KeQueryInterruptTime によって返される時間、操作の開始の 100 ナノ秒単位で示しています。</li>
<li><strong>TimeoutMilliseconds</strong>期間 NDIS、待機には、少なくともこのバグチェックをトリガーする前に示しています。</li>
<li><strong>TargetObject</strong>プロトコル、フィルター モジュール、またはで待機している NDIS ミニポート アダプターへのハンドルします。 実行 <strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">! ndiskd.protocol</a></strong>、  <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd.filter</a></strong>、または <strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd.netadapter</a></strong>詳細については、このハンドルを使用します。</li>
<li><strong>PrimaryThread</strong> NDIS が、操作を開始したスレッドです。 通常、操作が非同期的に処理される場合に、スレッドを他の場所で及ぼしてが可能性がありますが、検索するには、まずは、します。</li>
</ul></td>
<td align="left"><p>パラメーター 4 の値は、パラメーター 2 の値によって異なります。 この一覧の各番号は、パラメーター 2 で同じ番号に対応します。</p>
<ul>
<li>0x01 :0</li>
<li>0x02 :スタックのイベントの NET_PNP_EVENT_CODE します。 これらのコードの詳細については、次を参照してください <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event" data-raw-source="[NET_PNP_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)">NET_PNP_EVENT</a></strong>。</li>
<li>0x03 :スタックの表示の NDIS_STATUS コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x04 :0</li>
<li>パターン:0</li>
<li>0x12:スタックのイベントの NET_PNP_EVENT_CODE します。 使用可能な値は、このリストのアイテム 2 の値の前の一覧を参照してください。</li>
<li>0x13:スタックの表示の NDIS_STATUS コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x14:0</li>
<li>0x21:0</li>
<li>0x22:0</li>
<li>0x23:スタックの要求の OID コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x24:スタックの要求の OID コードです。 使用<strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! ndiskd.help</a></strong>にデコードします。</li>
<li>0x25:0</li>
<li>0x26:0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x30</p></td>
<td align="left"><p>NDIS_BUGCHECK_STUCK_NBL</p>
<p>ミニポート ドライバーは、NBL をしばらくの間、スタックに返されませんが。</p></td>
<td align="left"><p>ミニポート ブロックのアドレス。 実行<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">! ndiskd.minidriver</a></strong>詳細については、このアドレスを使用します。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

パラメーター 1 が、BUGCODE の具体的な原因を示す\_NDIS\_ドライバー\_LIVE\_バグチェックをダンプします。

<a name="remarks"></a>注釈
-------

NDIS が検出され、別のネットワーク ドライバーで重大な問題から回復しました。 システムは停止しませんが、この問題が接続の問題や致命的なバグチェックにより後で可能性があります。

このバグのコードは、Windows 8.1 と Windows の以降のバージョンでのみ発生します。

 

 




