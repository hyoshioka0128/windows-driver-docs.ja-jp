---
title: Bluetooth の付録
description: Bluetooth HCI のマイクロソフトによって定義された拡張機能の例と図が含まれています。
ms.assetid: 5C3C2479-03F9-4D33-94DA-3371D84C514B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50c566181f27f386cc1a0912e3044587e46e70f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580309"
---
# <a name="bluetooth-appendix"></a>Bluetooth の付録

このセクションには、Bluetooth HCI のマイクロソフトによって定義された拡張機能の例と図が含まれています。

## <a name="example-matching-patterns-for-hcivsmsftlemonitoradvertisement"></a>例:HCI_VS_MSFT_LE_Monitor_Advertisement のパターンに一致します。
この例では、受信した HCI_VS_MSFT_LE_Monitor_Advertisement コマンドとコマンドのパラメーターに対して 3 つの異なるアドバタイズ パケットの評価を示します。

HCI_VS_MSFT_LE_Monitor_Advertisement An HCI_VS_MSFT_LE_Monitor_Advertisement コマンドのコマンドは、コント ローラーによって受信され、次のパラメーターが含まれていますを受信します。

<table>
<tr>
<th>パラメーター</th>
<th>[値]</th>
<th></th>
</tr>
<tr>
<td>
<p><i>Subcommand_opcode</i></p>
</td>
<td>
<p>0x03</p>
</td>
<td>
<p>HCI_VS_MSFT_LE_Monitor_Advertisement のサブコマンドのオペコード</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_high</i></p>
</td>
<td>
<p>0x01</p>
</td>
<td>
<p>1dB</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_low</i></p>
</td>
<td>
<p>0xCE</p>
</td>
<td>
<p>-50dB</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_low_time_interval</i></p>
</td>
<td>
<p>0x05</p>
</td>
<td>
<p>5 秒</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_sampling_period</i></p>
</td>
<td>
<p>0 xff の場合</p>
</td>
<td>
<p>サンプリングなし</p>
</td>
</tr>
<tr>
<td>
<p><i>Condition_type</i></p>
</td>
<td>
<p>0x01</p>
</td>
<td>
<p><i>条件</i>がパターン</p>
</td>
</tr>
<tr>
<td rowspan="12">
<p><i>条件</i></p>
</td>
<td>
<p>0x02</p>
</td>
<td>
<p>2 つのパターンが一致する必要があります。</p>
</td>
</tr>
<tr>
<td>
<p>0x03</p>
</td>
<td>
<p>最初のパターン、広告の種類を含む、開始位置と長さ</p>
</td>
</tr>
<tr>
<td>
<p>0x01</p>
</td>
<td>
<p>広告の種類</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>次の広告の種類の開始位置</p>
</td>
</tr>
<tr>
<td>
<p>0x01</p>
</td>
<td>
<p>最初のパターンを照合します。</p>
</td>
</tr>
<tr>
<td>
<p>0x06</p>
</td>
<td>
<p>2 つ目のパターン、広告の種類を含む、開始位置と長さ</p>
</td>
</tr>
<tr>
<td>
<p>0 xff の場合</p>
</td>
<td>
<p>広告の種類 (製造元固有のデータ)</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>次の広告の種類の開始位置</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td rowspan="4">
<p>2 つ目のパターンを照合します。</p>
</td>
</tr>
<tr>
<td>
<p>0x06</p>
</td>
</tr>
<tr>
<td>
<p>0 xff の場合</p>
</td>
</tr>
<tr>
<td>
<p>0 xff の場合</p>
</td>
</tr>
</table>
<p> </p>
コント ローラーは、次の提供情報のパケットを受信します。


-    提供情報のパケット [A] 0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

-    提供情報のパケット [B] 0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0x01

-    提供情報のパケット [C] 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

</dd>
</dl>

### <a name="evaluating-match-for-advertisement-packet-a"></a>提供情報のパケット [A] の一致を評価します。

<table>
<tr>
<td>
<p>一致する最初のパターンの広告の種類</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>一致する最初のパターンの長さ</p>
</td>
<td>
<p>0x03 - 0x02 = 0x01 バイト</p>
</td>
</tr>
<tr>
<td>
<p>AD 型 0x01 の位置を 0x00 で照合されるパターン</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>0x01 広告の種類の 0x00 の位置にあるバイト</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>一致する 2 つ目のパターンの広告の種類</p>
</td>
<td>
<p>0 xff (製造元固有のデータ)</p>
</td>
</tr>
<tr>
<td>
<p>一致する 2 つ目のパターンの長さ</p>
</td>
<td>
<p>0x06 - 0x02 = 0x04 バイト</p>
</td>
</tr>
<tr>
<td>
<p>広告の種類 0 xff の位置を 0x00 で照合されるパターン</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td>
<p>広告の種類 0 xff の 0x00 の位置にあるバイト</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>判決を下せば:パス</b></p>
</td>
</tr>
</table>
  


### <a name="evaluating-match-for-advertisement-packet-b"></a>提供情報のパケット [B] の一致を評価します。
<table>
<tr>
<td>
<p>一致する最初のパターンの広告の種類</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>一致する最初のパターンの長さ</p>
</td>
<td>
<p>0x03 - 0x02 = 0x01 バイト</p>
</td>
</tr>
<tr>
<td>
<p>AD 型 0x01 の位置を 0x00 で照合されるパターン</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>0x01 広告の種類の 0x00 の位置にあるバイト</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>一致する 2 つ目のパターンの広告の種類</p>
</td>
<td>
<p>0 xff (製造元固有のデータ)</p>
</td>
</tr>
<tr>
<td>
<p>一致する 2 つ目のパターンの長さ</p>
</td>
<td>
<p>0x06 - 0x02 = 0x04 バイト</p>
</td>
</tr>
<tr>
<td>
<p>広告の種類 0 xff の位置を 0x00 で照合されるパターン</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0 xff の場合</b></p>
</td>
</tr>
<tr>
<td>
<p>広告の種類 0 xff の 0x00 の位置にあるバイト</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0x01</b></p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>判決を下せば:パス</b></p>
</td>
</tr>
</table>
 
### <a name="evaluating-match-for-advertisement-packet-c"></a>提供情報のパケット [C] の一致を評価します。
<table>
<tr>
<td>
<p>一致する最初のパターンの広告の種類</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>一致する最初のパターンの長さ</p>
</td>
<td>
<p>0x03 - 0x02 = 0x01 バイト</p>
</td>
</tr>
<tr>
<td>
<p>AD 型 0x01 の位置を 0x00 で照合されるパターン</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>0x01 広告の種類の 0x00 の位置にあるバイト</p>
</td>
<td>
<p>定義されていません。 提供情報には、AD 型 0x01 のデータはありません。</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>判決を下せば:失敗</b></p>
</td>
</tr>
</table>

## <a name="example-advertisement-monitoring"></a>例:提供情報の監視

この例では、RSSI 提供情報を監視しています。 指定した条件に一致する受信の提供情報の RSSI 値は、以下に示します。

<table>
<tr>
<th>回数</th>
<th>RSSI (dB)</th>
</tr>
<tr>
<td>1</td>
<td>-100</td>
</tr>
<tr>
<td>2</td>
<td>-90</td>
</tr>
<tr>
<td>3</td>
<td>-5</td>
</tr>
<tr>
<td>4</td>
<td>-15</td>
</tr>
<tr>
<td>5</td>
<td>-30</td>
</tr>
<tr>
<td>6</td>
<td>-15</td>
</tr>
<tr>
<td>7</td>
<td>-45</td>
</tr>
<tr>
<td>8</td>
<td>-20</td>
</tr>
<tr>
<td>9</td>
<td>-35</td>
</tr>
<tr>
<td>10</td>
<td>-45</td>
</tr>
<tr>
<td>11</td>
<td>-70</td>
</tr>
<tr>
<td>12</td>
<td>-85</td>
</tr>
<tr>
<td>13</td>
<td>-85</td>
</tr>
<tr>
<td>14</td>
<td>-85</td>
</tr>
<tr>
<td>15</td>
<td>-90</td>
</tr>
<tr>
<td>16</td>
<td>-90</td>
</tr>
<tr>
<td>17</td>
<td>-70</td>
</tr>
</table>
<p> </p>
<table>


<table>
<tr>
<th>パラメーター</th>
<th>[値]</th>
</tr>
<tr>
<td><i>RSSI_threshold_high</i></td>
<td>-10 db</td>
</tr>
<tr>
<td><i>RSSI_threshold_low</i></td>
<td>-80dB</td>
</tr>
<tr>
<td><i>RSSI_threshold_low_time_interval</i></td>
<td>3 秒</td>
</tr>
<tr>
<td><i>RSSI_sampling_period</i></td>
<td>2 秒</td>
</tr>
</table>

</p><img src="images/HCI_Example_Advertisement_Monitoring.png" alt="Advertisement monitoring graph"/><p>

提供情報 RSSI が一度に 3 RSSI_threshold_high より大きいです。 サンプリングの定期的なタイマーは、3 時に開始されます。 2 秒ごとにでは、定期的なタイマーの有効期限が切れるされ、スタックに受信した提供情報の平均 RSSI 値が反映されます。

提供情報 RSSIs の平均値がこの時間中に受信した定期的なタイマーは 5 時に期限が切れると、(-23dB) がスタックに伝達されます。

この期間中に受信した RSSIs 提供情報の平均値を下回って RSSI_threshold_low 定期的なタイマーは、13 時に期限が切れると、(-80dB)。 提供情報 RSSI (-85 dB) の平均は、ホストに反映する必要があります。

RSSI_threshold_low_time_interval はインスタント 15 に期限が切れると、ホストの - 85dB RSSI に提供情報が反映されます。 この例では、ホストには、さらに提供情報は送信されません。

 ## <a name="flowchart-advertisement-and-white-list-filtering"></a>フローチャート:提供情報とホワイト リストのフィルター処理

このフローチャートは、提供情報のフィルター処理と、提供情報を受信したときに、ホワイト リストがフィルター処理の例をコント ローラーの実装を提供します。

コント ローラー ロジックを実装できますこの異なる方法で、ホストは提供情報の通知を受け取る場合に限り、または </mshelp:link tabindex =「0」keywords="bltooth.hci_vs_msft_le_monitor_device_event"><b>HCI_VS_MSFT_LE_Monitor_Device_Event</b><//mshelp:link > フローチャートとして指定します。

<p><img src="images/HCI_Filtering_Flowchart.png" alt="Microsoft HCI extension filtering flowchart"/></p>


## <a name="sequence-diagram-propagate-scan-response-associated-with-advertisement"></a>シーケンス図に示します。スキャンの応答に関連付けられた提供情報を伝達します。

シーケンス図に示します。スキャンの応答に関連付けられた提供情報を伝達します。

このシーケンス図では、アクティブなスキャンが有効にすると、提供情報のフィルターに適合する提供情報に関連付けられている伝達スキャン応答を示します。
のみ、次の図は、コント ローラーとホスト間でイベントの順序を表示して、コント ローラーと、特定のデバイス間でイベントが表示されません。
提供情報があることを前提としています<i>A</i>の提供情報のフィルター処理、および提供情報を満たす<i>B</i>提供情報のフィルターを満たしていません。
<p> <img src="images/HCI_Propagate_Scan_Sequence.png" alt="HCI propagate scan sequence diagram"/></p>
