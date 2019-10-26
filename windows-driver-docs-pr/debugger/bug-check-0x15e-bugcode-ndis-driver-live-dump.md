---
title: バグチェック 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
description: BUGCODE_NDIS_DRIVER_LIVE_DUMP バグコードには、0x0000015E という値が指定されています。 このバグコードは、NDIS がライブカーネルダンプをキャプチャしたことを示しています。 この状況では、NDIS はバグチェックを生成しません。
ms.assetid: 3663A955-A1D7-4880-BD83-0976012F2CB1
keywords:
- バグチェック 0x15E BUGCODE_NDIS_DRIVER_LIVE_DUMP
- BUGCODE_NDIS_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_NDIS_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9eaa78f3d89f85e63406ffdfbd25bafe6a934e33
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892689"
---
# <a name="bug-check-0x15e-bugcode_ndis_driver_live_dump"></a>バグチェック 0x15E: コード\_NDIS\_ドライバー\_ライブ\_ダンプ


バグコード\_NDIS\_ドライバー\_ライブ\_ダンプバグコードには、0x0000015E という値が指定されています。 このバグコードは、NDIS がライブカーネルダンプをキャプチャしたことを示しています。 この状況では、NDIS はバグチェックを生成しません。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bugcode_ndis_driver-parameters"></a>\_NDIS\_ドライバーパラメーターのバグコード


パラメーター1は違反の種類を示します。 他のパラメーターの意味は、パラメーター1の値によって異なります。 パラメーターの値が "0" の場合、これは使用されないことを意味します。

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
<th align="left">パラメーター1</th>
<th align="left">パラメーター1の値とエラーの原因</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>NDIS_BUGCHECK_MINIPORT_FATAL_ERROR</p>
<p>ミニポートドライバーで致命的なエラーが発生し、再列挙が要求されました。</p></td>
<td align="left"><p>ミニポートブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">ミニドライバー</a></strong>を実行してください。</p></td>
<td align="left"><p>ミニポートの物理デバイスオブジェクト (PDO) のアドレス</p></td>
<td align="left"><p>このライブダンプが実行される原因となった致命的なエラーです。 設定可能な値:</p>
<ol>
<li>70: ユーザーモードにより発生しました</li>
<li>71: NdisMRemoveMiniport によって発生しました <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport" data-raw-source="[NdisMRemoveMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismremoveminiport)"></a></strong></li>
<li>72: <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex" data-raw-source="[NdisIMInitializeDeviceInstanceEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)">NdisIMInitializeDeviceInstanceEx</a></strong>が失敗したために発生しました</li>
<li>73: <em><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart" data-raw-source="[MiniportRestart](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)">Miniportrestart</a></em>が失敗したために発生しました</li>
<li>74: <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER (D0)](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER (D0)</a>要求が失敗したために発生しました</li>
<li>75: <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power" data-raw-source="[OID_PNP_SET_POWER (Dx)](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)">OID_PNP_SET_POWER (Dx)</a>要求が失敗したために発生しました</li>
</ol></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>NDIS_BUGCHECK_WATCHDOG</p>
<p>ネットワークスタックを管理しようとしましたが、時間がかかりすぎています。 NDIS は他のドライバーを呼び出すと、呼び出しが即座に完了するようにウォッチドッグタイマーを開始します。 呼び出しに時間がかかる場合、NDIS はバグチェックを挿入します。</p>
<p>これは、単純なデッドロックが原因である可能性があります。 "! Stack 2 ndis" を使用するか、疑わしいと思われるスレッドがあるかどうかを確認します。 NDIS_WATCHDOG_TRIAGE_BLOCK から PrimaryThread に特に注意を払ってください。</p>
<p>NBLs が失われたことが原因である可能性があります。その場合は、 <strong><a href="-ndiskd-pendingnbls.md" data-raw-source="[!ndiskd.pendingnbls](-ndiskd-pendingnbls.md)">pendingnbls</a></strong>が役に立ちます。 <strong><a href="-ndiskd-oid.md" data-raw-source="[!ndiskd.oid](-ndiskd-oid.md)">! Ndiskd oid</a></strong>を使用してスタックされている oid を確認します。</p></td>
<td align="left"><p>操作に時間がかかりすぎました。 設定可能な値:</p>
<ul>
<li><p>0x01: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_PAUSE</p>
<p>プロトコルドライバーの一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x02: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_NETPNPEVENT</p>
<p>プロトコルドライバーに NET_PNP_EVENT_NOTIFICATION を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x03: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_STATUS_INDICATION</p>
<p>プロトコルドライバーに状態の通知を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x04: NDIS_BUGCHECK_WATCHDOG_PROTOCOL_UNBIND</p>
<p>プロトコルドライバーのバインド解除中にタイムアウトが発生しました。</p></li>
<li><p>0x11 : NDIS_BUGCHECK_WATCHDOG_FILTER_PAUSE</p>
<p>フィルタードライバーの一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x12 : NDIS_BUGCHECK_WATCHDOG_FILTER_NETPNPEVENT</p>
<p>フィルタードライバーに NET_PNP_EVENT_NOTIFICATION を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x13: NDIS_BUGCHECK_WATCHDOG_FILTER_STATUS_INDICATION</p>
<p>フィルタードライバーへのステータスの通知を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x14: NDIS_BUGCHECK_WATCHDOG_FILTER_DETACH</p>
<p>フィルタードライバーのデタッチ中にタイムアウトが発生しました。</p></li>
<li><p>0x21: NDIS_BUGCHECK_WATCHDOG_MINIPORT_PAUSE</p>
<p>ミニポートアダプターの一時停止中にタイムアウトが発生しました。</p></li>
<li><p>0x22: NDIS_BUGCHECK_WATCHDOG_MINIPORT_HALT</p>
<p>ミニポートアダプターの停止中にタイムアウトが発生しました。</p></li>
<li><p>0x23: NDIS_BUGCHECK_WATCHDOG_MINIPORT_OID</p>
<p>ミニポートアダプターに OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x24: NDIS_BUGCHECK_WATCHDOG_FILTER_OID</p>
<p>フィルタードライバーに OID 要求を配信中にタイムアウトが発生しました。</p></li>
<li><p>0x25: NDIS_BUGCHECK_WATCHDOG_MINIPORT_IDLE</p>
<p>ミニポートアダプターのアイドル状態中にタイムアウトが発生しました。</p></li>
<li><p>0x26: NDIS_BUGCHECK_WATCHDOG_CANCEL_IDLE</p>
<p>ミニポートアダプターでアイドル状態の要求を取り消しているときにタイムアウトが発生しました。</p></li>
</ul></td>
<td align="left"><p>Ndis にキャストします。NDIS_WATCHDOG_TRIAGE_BLOCK. 便利なフィールド:</p>
<ul>
<li><strong>StartTime</strong>は、KeQueryInterruptTime によって返される操作の開始時刻を100ナノ秒単位で表示します。</li>
<li><strong>Timeoutmilliseconds</strong>は、このバグチェックをトリガーする前に、少なくとも NDIS が待機した時間を示します。</li>
<li><strong>TargetObject</strong>は、NDIS が待機しているプロトコル、フィルターモジュール、またはミニポートアダプターへのハンドルです。 詳細については、このハンドルを使用して<strong><a href="-ndiskd-protocol.md" data-raw-source="[!ndiskd.protocol](-ndiskd-protocol.md)">! ndiskd protocol</a></strong>、 <strong><a href="-ndiskd-filter.md" data-raw-source="[!ndiskd.filter](-ndiskd-filter.md)">! ndiskd filter</a></strong>、または<strong><a href="-ndiskd-netadapter.md" data-raw-source="[!ndiskd.netadapter](-ndiskd-netadapter.md)">! ndiskd netadapter</a></strong>を実行してください。</li>
<li><strong>Primarythread</strong>は、NDIS が操作を開始したスレッドです。 通常、これは最初に確認する場所ですが、操作が非同期に処理されている場合、スレッドは他の場所に存在する可能性があります。</li>
</ul></td>
<td align="left"><p>パラメーター4の値は、パラメーター2の値に依存します。 この一覧の各数値は、パラメーター2の同じ数値に対応しています。</p>
<ul>
<li>0x01: 0</li>
<li>0x02: スタックイベントの NET_PNP_EVENT_CODE。 これらのコードの詳細については、「 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event" data-raw-source="[NET_PNP_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)">NET_PNP_EVENT</a></strong>.」を参照してください。</li>
<li>0x03: スタック表示の NDIS_STATUS コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x04: 0</li>
<li>0x11: 0</li>
<li>0x12: スタックイベントの NET_PNP_EVENT_CODE。 使用可能な値については、この一覧の項目2の値の前の一覧を参照してください。</li>
<li>0x13: スタック表示の NDIS_STATUS コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x14: 0</li>
<li>0x21: 0</li>
<li>0x22: 0</li>
<li>0x23: スタック要求の OID コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x24: スタック要求の OID コード。 <strong><a href="-ndiskd-help.md" data-raw-source="[!ndiskd.help](-ndiskd-help.md)">! Ndiskd help</a></strong>を使用してデコードしてください。</li>
<li>0x25: 0</li>
<li>0x26: 0</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>0x30</p></td>
<td align="left"><p>NDIS_BUGCHECK_STUCK_NBL</p>
<p>ミニポートドライバーは、しばらくの間、スタックに NBL を返しませんでした。</p></td>
<td align="left"><p>ミニポートブロックのアドレス。 詳細については、このアドレスを使用して<strong><a href="-ndiskd-minidriver.md" data-raw-source="[!ndiskd.minidriver](-ndiskd-minidriver.md)">ミニドライバー</a></strong>を実行してください。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 パラメーター1は、バグコード\_NDIS\_ドライバーの特定の原因を示し\_ライブ\_ダンプのバグチェックを行います。

<a name="remarks"></a>注釈
-------

NDIS は、別のネットワークドライバーの重大な問題を検出し、回復しました。 システムは停止されていませんが、この問題によって接続の問題または致命的なバグチェックが発生する可能性があります。

このバグコードは、Windows 8.1 以降のバージョンの Windows でのみ発生します。

 

 




