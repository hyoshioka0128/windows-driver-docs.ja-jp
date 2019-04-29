---
title: シリアル I/O 要求インターフェイス
description: シリアル コント ローラーで、クライアントのポートに接続されている周辺機器を制御するには、アプリケーションまたは周辺機器のデバイス ドライバーは、ポートに I/O 要求を送信します。
ms.assetid: D536A0EC-2B8B-491B-8A14-656F4B5A3843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6e2ce72e1b26843a1714b6483aaf68b7417793d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327418"
---
# <a name="serial-io-request-interface"></a>シリアル I/O 要求インターフェイス


シリアル コント ローラーで、クライアントのポートに接続されている周辺機器を制御するには、アプリケーションまたは周辺機器のデバイス ドライバーは、ポートに I/O 要求を送信します。 クライアントを使って[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff546904)と[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff546883)データを送信し、シリアル ポートから受信したデータを要求します。 さらに、Windows には、一連の定義されています。[シリアル I/O 制御](https://msdn.microsoft.com/library/windows/hardware/ff547466)シリアル ポートを構成するクライアントが使用できる要求 (Ioctl)。

シリアル**IRP\_MJ\_* XXX*** シリアル I/O 要求インターフェイスは、さまざまなデバイスのシリアル コント ローラーでサポートされている要求とシリアル Ioctl 形成します。 SerCx2 または SerCx とシリアル コント ローラーの拡張機能に基づいたドライバーの組み合わせと、以下のようドライバーによって、このインターフェイスはサポートされています。

SerCx2、SerCx、および際に、同じシリアル Ioctl の多くをサポートします。 ただし、SerCx2、SerCx、および以下のように指定された Ioctl のさまざまなサブセットをサポート[シリアル デバイスに対する制御要求](https://msdn.microsoft.com/library/windows/hardware/ff547466)します。 次の表は、Ioctl SerCx2、SerCx、およびスタックでサポートされているのサブセットをまとめたものです。 A**はい**テーブル内のエントリは、シリアル フレームワークの拡張機能またはドライバーが、対応する、IOCTL をサポートしていることを示します、**いいえ**エントリはしないことを示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>シリアル IOCTL</th>
<th>SerCx2</th>
<th>SerCx</th>
<th>スタック</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406621" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406621)"><strong>IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>X</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546538" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLEAR_STATS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546538)"><strong>IOCTL_SERIAL_CLEAR_STATS</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546541" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_DTR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546541)"><strong>IOCTL_SERIAL_CLR_DTR</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546545" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_RTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546545)"><strong>IOCTL_SERIAL_CLR_RTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546548" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CONFIG_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546548)"><strong>IOCTL_SERIAL_CONFIG_SIZE</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546554" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_BAUD_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546554)"><strong>IOCTL_SERIAL_GET_BAUD_RATE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546558" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_CHARS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546558)"><strong>IOCTL_SERIAL_GET_CHARS</strong></a></p></td>
<td><p>注 2 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546562" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_COMMSTATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546562)"><strong>IOCTL_SERIAL_GET_COMMSTATUS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546566" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_DTRRTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546566)"><strong>IOCTL_SERIAL_GET_DTRRTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546574" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_HANDFLOW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546574)"><strong>IOCTL_SERIAL_GET_HANDFLOW</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546582" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_LINE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546582)"><strong>IOCTL_SERIAL_GET_LINE_CONTROL</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546591" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546591)"><strong>IOCTL_SERIAL_GET_MODEM_CONTROL</strong> </a> (注 4 を参照)</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546587" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEMSTATUS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546587)"><strong>IOCTL_SERIAL_GET_MODEMSTATUS</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546597" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_PROPERTIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546597)"><strong>IOCTL_SERIAL_GET_PROPERTIES</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546600" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_STATS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546600)"><strong>IOCTL_SERIAL_GET_STATS</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546604" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_TIMEOUTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546604)"><strong>IOCTL_SERIAL_GET_TIMEOUTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546610" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_WAIT_MASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546610)"><strong>IOCTL_SERIAL_GET_WAIT_MASK</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546620" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_IMMEDIATE_CHAR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546620)"><strong>IOCTL_SERIAL_IMMEDIATE_CHAR</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546649" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_LSRMST_INSERT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546649)"><strong>IOCTL_SERIAL_LSRMST_INSERT</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546655" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_PURGE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546655)"><strong>IOCTL_SERIAL_PURGE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546671" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_RESET_DEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546671)"><strong>IOCTL_SERIAL_RESET_DEVICE</strong> </a> (注 5 を参照)</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546672" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BAUD_RATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546672)"><strong>IOCTL_SERIAL_SET_BAUD_RATE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546680" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_OFF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546680)"><strong>IOCTL_SERIAL_SET_BREAK_OFF</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546685" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_ON&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546685)"><strong>IOCTL_SERIAL_SET_BREAK_ON</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546688" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_CHARS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546688)"><strong>IOCTL_SERIAL_SET_CHARS</strong></a></p></td>
<td><p>注 2 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546696" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_DTR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546696)"><strong>IOCTL_SERIAL_SET_DTR</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546720" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_FIFO_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546720)"><strong>IOCTL_SERIAL_SET_FIFO_CONTROL</strong></a></p></td>
<td><p>注 1 を参照してください。</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546736" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_HANDFLOW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546736)"><strong>IOCTL_SERIAL_SET_HANDFLOW</strong> </a> (注 3 を参照)</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546740" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_LINE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546740)"><strong>IOCTL_SERIAL_SET_LINE_CONTROL</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546748" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_MODEM_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546748)"><strong>IOCTL_SERIAL_SET_MODEM_CONTROL</strong> </a> (注 4 を参照)</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546754" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_QUEUE_SIZE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546754)"><strong>IOCTL_SERIAL_SET_QUEUE_SIZE</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546760" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_RTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546760)"><strong>IOCTL_SERIAL_SET_RTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546772" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_TIMEOUTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546772)"><strong>IOCTL_SERIAL_SET_TIMEOUTS</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546780" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_WAIT_MASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546780)"><strong>IOCTL_SERIAL_SET_WAIT_MASK</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546784" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XOFF&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546784)"><strong>IOCTL_SERIAL_SET_XOFF</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546793" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XON&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546793)"><strong>IOCTL_SERIAL_SET_XON</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546805" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_WAIT_ON_MASK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546805)"><strong>IOCTL_SERIAL_WAIT_ON_MASK</strong></a></p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546812" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_XOFF_COUNTER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546812)"><strong>IOCTL_SERIAL_XOFF_COUNTER</strong></a></p></td>
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>〇</p></td>
</tr>
</tbody>
</table>

 

**メモ**

1.  SerCx2 は可能性があります。 またはコント ローラーのシリアル ドライバーの実装とシリアル コント ローラーのハードウェアの機能によってこの IOCTL をサポートしていません。

2.  SerCx2 は特殊文字をサポートしていません。 SerCx2 が完了すると常に、 **IOCTL\_シリアル\_設定\_CHARS**状態が、要求\_成功の状態のコードはない特殊文字を設定またはその他の操作を実行この要求に応答します。 **IOCTL\_シリアル\_取得\_CHARS** SerCx2 のすべての文字値の設定を要求、 [**シリアル\_CHARS** ](https://msdn.microsoft.com/library/windows/hardware/jj673020)を null、構造体であり、状態が、要求が完了すると\_成功状態コード。

3.  SerCx2 と SerCx に対して定義されているフラグのサブセットのみをサポート、 **FlowReplace**と**ControlHandShake**のメンバー、**シリアル\_HANDFLOW**構造体。 以下のようには、すべてのこれらのフラグがサポートしています。 詳細については、次を参照してください。 [**シリアル\_HANDFLOW**](https://msdn.microsoft.com/library/windows/hardware/jj680685)します。

4.  **IOCTL\_シリアル\_取得\_モデム\_コントロール**と**IOCTL\_シリアル\_設定\_モデム\_コントロール**要求は、主に、ハードウェアのテストに使用します。 モデムの管理操作を登録する標準的なレイアウトが定義されていません。 モデム コントロール シリアル コント ローラーの特定のハードウェア機能に依存させること自体の Ioctl リスクを使用して、周辺機器のドライバーです。

5.  スタックのドライバーが完了すると常に、 **IOCTL\_シリアル\_リセット\_デバイス**状態要求\_成功した場合、演算を実行しないこの要求に応答します。 SerCx2 および SerCx はサポートされません**IOCTL\_シリアル\_リセット\_デバイス**要求し、これらの要求の状態を常に完了\_いない\_実装されていません。

詳細については**IOCTL\_シリアル\_* XXX***、要求を参照してください[シリアル デバイスに対する制御要求](https://msdn.microsoft.com/library/windows/hardware/ff547466)します。 読み取りし、書き込みシリアル コント ローラーの要求についての詳細についてを参照してください。[シリアルの主要な I/O 要求](https://msdn.microsoft.com/library/windows/hardware/ff547484)します。

 

 




