---
title: ポート モニター サーバー DLL 関数
description: ポート モニター サーバー DLL 関数
ms.assetid: ffbcaaaa-7f9d-4b29-b939-189e10174074
keywords:
- ポート モニターを WDK の印刷、関数
- サーバー DLL ポート モニター機能 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1723b67b82c0b63321d575c0a865e21eccaf21cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580524"
---
# <a name="port-monitor-server-dll-functions"></a>ポート モニター サーバー DLL 関数





次の表には、ポート監視のサーバー DLL を定義する必要がある関数が一覧表示します。

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
<td><p>DLL エントリ ポイントと通常呼ばれる<strong>DllMain</strong>、これは、Microsoft Windows SDK ドキュメントで説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545975" data-raw-source="[&lt;strong&gt;ClosePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545975)"><strong>ClosePort</strong></a></p></td>
<td><p>プリンター接続がない場合は、ポートを閉じます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548742" data-raw-source="[&lt;strong&gt;EndDocPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548742)"><strong>EndDocPort</strong></a></p></td>
<td><p>ポートの終了の印刷ジョブのタスクを実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548754" data-raw-source="[&lt;strong&gt;EnumPorts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548754)"><strong>EnumPorts</strong></a></p></td>
<td><p>サーバー上の印刷可能なポートを列挙します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551605" data-raw-source="[&lt;strong&gt;InitializePrintMonitor2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551605)"><strong>InitializePrintMonitor2</strong></a></p></td>
<td><p>印刷のモニターを初期化し、インスタンス ハンドルを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559593" data-raw-source="[&lt;strong&gt;OpenPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559593)"><strong>OpenPort</strong></a></p></td>
<td><p>プリンター ポートを開きます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559596" data-raw-source="[&lt;strong&gt;OpenPortEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559596)"><strong>OpenPortEx</strong></a></p></td>
<td><p>プリンター ポートを開きます。 (言語モニターのみ)</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561909" data-raw-source="[&lt;strong&gt;ReadPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561909)"><strong>ReadPort</strong></a></p></td>
<td><p>プリンター ポートからデータを読み取ります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562710" data-raw-source="[&lt;strong&gt;StartDocPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562710)"><strong>StartDocPort</strong></a></p></td>
<td><p>ポートでの印刷ジョブの開始に必要なタスクを実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563792" data-raw-source="[&lt;strong&gt;WritePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563792)"><strong>WritePort</strong></a></p></td>
<td><p>プリンター ポートにデータを書き込みます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564254" data-raw-source="[&lt;strong&gt;XcvClosePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564254)"><strong>XcvClosePort</strong></a></p></td>
<td><p>ポート管理が完了した後は、ポートを閉じます。 Windows 2000 以降のオペレーティング システムの NT ベースのバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564258" data-raw-source="[&lt;strong&gt;XcvDataPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564258)"><strong>XcvDataPort</strong></a></p></td>
<td><p>ポートの管理タスクを処理します。 Windows 2000 以降のオペレーティング システムの NT ベースのバージョンで使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564259" data-raw-source="[&lt;strong&gt;XcvOpenPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564259)"><strong>XcvOpenPort</strong></a></p></td>
<td><p>管理のためのポートを開きます。 Windows 2000 以降のオペレーティング システムの NT ベースのバージョンで使用できます。</p></td>
</tr>
</tbody>
</table>

 

次のポート モニター サーバー DLL の関数は省略可能です。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550506" data-raw-source="[&lt;strong&gt;GetPrinterDataFromPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550506)"><strong>GetPrinterDataFromPort</strong></a></p></td>
<td><p>ポートのドライバーに、I/O 制御コードを送信し、結果を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562071" data-raw-source="[&lt;strong&gt;SendRecvBidiDataFromPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562071)"><strong>SendRecvBidiDataFromPort</strong></a></p></td>
<td><p>アプリケーションとプリンターまたはプリント サーバーの間の双方向通信をサポートしています。 Windows XP 以降を使用できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562630" data-raw-source="[&lt;strong&gt;SetPortTimeOuts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562630)"><strong>SetPortTimeOuts</strong></a></p></td>
<td><p>ポートを開くには、タイムアウト値を設定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562646" data-raw-source="[&lt;strong&gt;Shutdown&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562646)"><strong>Shutdown</strong></a></p></td>
<td><p>モニターのインスタンスを削除します。 この関数は、クラスターのサポートに必要です。</p></td>
</tr>
</tbody>
</table>

 

 

 




