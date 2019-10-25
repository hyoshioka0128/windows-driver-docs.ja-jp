---
title: ポート モニター サーバー DLL 関数
description: ポート モニター サーバー DLL 関数
ms.assetid: ffbcaaaa-7f9d-4b29-b939-189e10174074
keywords:
- ポートモニター WDK print、functions
- サーバー DLL ポートモニター関数 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe80c20139b5b116cd69fb9a3519a0f47391e1e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842351"
---
# <a name="port-monitor-server-dll-functions"></a>ポート モニター サーバー DLL 関数





次の表に、ポートモニターサーバー DLL で定義する必要がある関数を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DllEntryPoint</strong></p></td>
<td><p>DLL のエントリポイント。通常は、Microsoft Windows SDK のドキュメントで説明されている<strong>DllMain</strong>と呼ばれます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport" data-raw-source="[&lt;strong&gt;ClosePort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport)"><strong>ClosePort</strong></a></p></td>
<td><p>プリンターが接続されていない場合は、ポートを閉じます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff548742(v=vs.85)" data-raw-source="[&lt;strong&gt;EndDocPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))"><strong>EndDocPort</strong></a></p></td>
<td><p>ポートで印刷ジョブ終了タスクを実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff548754(v=vs.85)" data-raw-source="[&lt;strong&gt;EnumPorts&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548754(v=vs.85))"><strong>EnumPorts</strong></a></p></td>
<td><p>サーバーでの印刷に使用できるポートを列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2" data-raw-source="[&lt;strong&gt;InitializePrintMonitor2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)"><strong>InitializePrintMonitor2</strong></a></p></td>
<td><p>印刷モニターを初期化し、インスタンスハンドルを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport" data-raw-source="[&lt;strong&gt;OpenPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)"><strong>OpenPort</strong></a></p></td>
<td><p>プリンターポートを開きます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff559596(v=vs.85)" data-raw-source="[&lt;strong&gt;OpenPortEx&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85))"><strong>OpenPortEx</strong></a></p></td>
<td><p>プリンターポートを開きます。 (言語モニターのみ)</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport" data-raw-source="[&lt;strong&gt;ReadPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)"><strong>ReadPort</strong></a></p></td>
<td><p>プリンターポートからデータを読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562710(v=vs.85)" data-raw-source="[&lt;strong&gt;StartDocPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))"><strong>StartDocPort</strong></a></p></td>
<td><p>ポートで印刷ジョブを開始するために必要なタスクを実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport" data-raw-source="[&lt;strong&gt;WritePort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)"><strong>WritePort</strong></a></p></td>
<td><p>プリンターポートにデータを書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport" data-raw-source="[&lt;strong&gt;XcvClosePort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvcloseport)"><strong>XcvClosePort</strong></a></p></td>
<td><p>ポートの管理が完了した後、ポートを閉じます。 Windows 2000 以降の NT ベースのオペレーティングシステムバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport" data-raw-source="[&lt;strong&gt;XcvDataPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvdataport)"><strong>XcvDataPort</strong></a></p></td>
<td><p>ポート管理タスクを処理します。 Windows 2000 以降の NT ベースのオペレーティングシステムバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport" data-raw-source="[&lt;strong&gt;XcvOpenPort&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-xcvopenport)"><strong>XcvOpenPort</strong></a></p></td>
<td><p>管理のためにポートを開きます。 Windows 2000 以降の NT ベースのオペレーティングシステムバージョンで使用できます。</p></td>
</tr>
</tbody>
</table>

 

次のポート監視サーバーの DLL 関数は省略可能です。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>関数名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff550506(v=vs.85)" data-raw-source="[&lt;strong&gt;GetPrinterDataFromPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))"><strong>GetPrinterDataFromPort</strong></a></p></td>
<td><p>I/o 制御コードをポートドライバーに送信し、その結果を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562071(v=vs.85)" data-raw-source="[&lt;strong&gt;SendRecvBidiDataFromPort&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))"><strong>SendRecvBidiDataFromPort</strong></a></p></td>
<td><p>アプリケーションとプリンターまたはプリントサーバー間の双方向通信をサポートします。 Windows XP 以降で使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562630(v=vs.85)" data-raw-source="[&lt;strong&gt;SetPortTimeOuts&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562630(v=vs.85))"><strong>SetPortTimeOuts</strong></a></p></td>
<td><p>開いているポートのタイムアウト値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/previous-versions/ff562646(v=vs.85)" data-raw-source="[&lt;strong&gt;Shutdown&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff562646(v=vs.85))"><strong>シャットダウン</strong></a></p></td>
<td><p>モニターインスタンスを削除します。 この機能は、クラスターのサポートに必要です。</p></td>
</tr>
</tbody>
</table>

 

 

 




