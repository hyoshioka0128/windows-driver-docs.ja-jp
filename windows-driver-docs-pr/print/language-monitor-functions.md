---
title: 言語モニター関数
description: 言語モニター関数
ms.assetid: ffe1a52f-69cc-4346-945f-3f1bc0a1a91e
keywords:
- 言語は、WDK の印刷、機能を監視します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5725011b1ed8acaba9da94ad920ed7d2316c100b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388100"
---
# <a name="language-monitor-functions"></a>言語モニター関数





次の表には、言語モニターを定義する必要がある関数が一覧表示します。

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
<td><p>それに接続されているプリンターが存在しない場合は、ポートを閉じます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548742" data-raw-source="[&lt;strong&gt;EndDocPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548742)"><strong>EndDocPort</strong></a></p></td>
<td><p>ポートの終了の印刷ジョブのタスクを実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550506" data-raw-source="[&lt;strong&gt;GetPrinterDataFromPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550506)"><strong>GetPrinterDataFromPort</strong></a></p></td>
<td><p>任意。 レジストリに格納されている値に使用するポートをポーリングします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551605" data-raw-source="[&lt;strong&gt;InitializePrintMonitor2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551605)"><strong>InitializePrintMonitor2</strong></a></p></td>
<td><p>印刷のモニターを初期化し、インスタンス ハンドルを返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559596" data-raw-source="[&lt;strong&gt;OpenPortEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559596)"><strong>OpenPortEx</strong></a></p></td>
<td><p>新しく接続されたプリンターのポートを開きます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561909" data-raw-source="[&lt;strong&gt;ReadPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561909)"><strong>ReadPort</strong></a></p></td>
<td><p>プリンター ポートからデータを読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562071" data-raw-source="[&lt;strong&gt;SendRecvBidiDataFromPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562071)"><strong>SendRecvBidiDataFromPort</strong></a></p></td>
<td><p>任意。 アプリケーションとプリンターまたはプリント サーバーの間の双方向通信をサポートしています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562646" data-raw-source="[&lt;strong&gt;Shutdown&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562646)"><strong>Shutdown</strong></a></p></td>
<td><p>任意。 モニターのインスタンスを削除します。 この関数は、クラスターのサポートに必要です。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff562710" data-raw-source="[&lt;strong&gt;StartDocPort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff562710)"><strong>StartDocPort</strong></a></p></td>
<td><p>ポートでの印刷ジョブの開始に必要なタスクを実行します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563792" data-raw-source="[&lt;strong&gt;WritePort&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563792)"><strong>WritePort</strong></a></p></td>
<td><p>プリンター ポートにデータを書き込みます。</p></td>
</tr>
</tbody>
</table>

 

 

 




