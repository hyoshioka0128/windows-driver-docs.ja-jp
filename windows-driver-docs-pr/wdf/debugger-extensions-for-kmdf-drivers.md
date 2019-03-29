---
title: Wdfkd.dll でのデバッガー拡張機能の概要
description: Windows Driver Kit (WDK) には、デバッガー拡張機能ライブラリ、Wdfkd.dll という名前が含まれています。
ms.assetid: 5a83ea58-5dbf-40a6-b4cb-9c330851fc33
keywords:
- 拡張機能の WDK デバッガー
- WDK KMDF のデバッガー拡張機能
- ドライバー WDK KMDF、デバッガーの拡張機能のデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a8312da48be5f01f540c50ed1aa1c0d29825172
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349959"
---
#  <a name="summary-of-debugger-extensions-in-wdfkddll"></a>Wdfkd.dll でのデバッガー拡張機能の概要


Windows Driver Kit (WDK) には、という名前のデバッガー拡張機能ライブラリが含まれています。 *Wdfkd.dll*します。 このライブラリには、バージョン 2 以降、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) の両方のドライバーをデバッグに使用できるデバッガー拡張機能のコマンドが含まれています。

各コマンドの詳細については、次を参照してください。 [ **Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)**](https://msdn.microsoft.com/library/windows/hardware/ff551876)します。 すべての利用可能なデバッガー拡張機能ライブラリの詳細についてで提供されるドキュメントを参照して、 [Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)パッケージ。

KMDF ドライバーでデバッグする方法を示すビデオ シリーズを検索する[ビデオ。KMDF ドライバーのデバッグ](debugging-kernel-mode-driver-framework-drivers.md)します。

UMDF 1.11 またはそれ以前のバージョンを使用するドライバーをデバッグする必要があります代わりに使用する、 *Wudfext.dll*デバッガー拡張機能ライブラリ。 詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークの拡張機能 (Wudfext.dll)](https://msdn.microsoft.com/library/windows/hardware/ff560030)します。

拡張機能のコマンドを*Wdfkd.dll*拡張機能ライブラリの提供が含まれます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">拡張</th>
<th align="left">説明</th>
<th align="left">フレームワーク</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565761" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhelp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565761)"><strong>!wdfkd.wdfhelp</strong></a></p></td>
<td align="left"><p>このデバッガー拡張機能の一覧が表示されます。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565672" data-raw-source="[&lt;strong&gt;!wdfkd.wdfchildlist&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565672)"><strong>!wdfkd.wdfchildlist</strong></a></p></td>
<td align="left"><p>子リストの状態とすべての子リスト内にあるデバイスの識別の説明に関する情報が表示されます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565675" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcollection&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565675)"><strong>!wdfkd.wdfcollection</strong></a></p></td>
<td align="left"><p>コレクションに含まれるオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565679" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcommonbuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565679)"><strong>!wdfkd.wdfcommonbuffer</strong></a></p></td>
<td align="left"><p>に関する情報を表示、<a href="using-common-buffers.md" data-raw-source="[common buffer object](using-common-buffers.md)">共通のバッファー オブジェクト</a>します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565682" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcrashdump&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565682)"><strong>!wdfkd.wdfcrashdump</strong></a></p></td>
<td align="left"><p>小さいメモリ ダンプから、使用可能な場合、framework のイベント ログのレコードを表示します。 フレームワークのイベント ログ レコードがある場合は<a href="registry-values-for-debugging-kmdf-drivers.md" data-raw-source="[ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)">ForceLogsInMiniDump</a>レジストリに設定されている場合、またはフレームワークが、ドライバーにバグ チェックが原因となったことを判断することができます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565686" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevext&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565686)"><strong>!wdfkd.wdfdevext</strong></a></p></td>
<td align="left"><p>関連付けられている WDFDEVICE に型指定されたオブジェクトのハンドルが表示されます、 <strong>DeviceExtension</strong>メンバーの Microsoft Windows Driver Model (WDM) <a href="https://msdn.microsoft.com/library/windows/hardware/ff543147" data-raw-source="[&lt;strong&gt;DEVICE_OBJECT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543147)"> <strong>DEVICE_OBJECT</strong> </a>構造体。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565703" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565703)"><strong>!wdfkd.wdfdevice</strong></a></p></td>
<td align="left"><p>WDFDEVICE に型指定されたハンドルに関連付けられている情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265378" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdeviceinterrupts&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265378)"><strong>!wdfkd.wdfdeviceinterrupts</strong></a></p></td>
<td align="left"><p>指定したデバイス ハンドルのすべての割り込みオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565715" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevicequeues&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565715)"><strong>!wdfkd.wdfdevicequeues</strong></a></p></td>
<td align="left"><p>指定されたデバイスに属するキュー オブジェクトのすべてに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565717" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenabler&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565717)"><strong>!wdfkd.wdfdmaenabler</strong></a></p></td>
<td align="left"><p>に関する情報を表示、 <a href="framework-dma-objects.md" data-raw-source="[DMA enabler object](framework-dma-objects.md)">DMA イネーブラー オブジェクト</a>、およびその関連付けられた DMA トランザクション オブジェクトと共通のバッファー オブジェクト。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565719" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenablers&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565719)"><strong>!wdfkd.wdfdmaenablers</strong></a></p></td>
<td align="left"><p>すべての DMA イネーブラー オブジェクト、DMA トランザクション オブジェクト、および指定したデバイス オブジェクトに関連付けられている共通のバッファー オブジェクトの概要を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565721" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmatransaction&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565721)"><strong>!wdfkd.wdfdmatransaction</strong></a></p></td>
<td align="left"><p>WDF ダイレクト メモリ アクセス (DMA) トランザクション オブジェクトについての情報を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565724" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdriverinfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565724)"><strong>!wdfkd.wdfdriverinfo</strong></a></p></td>
<td align="left"><p>オブジェクトのハンドルの階層を変更したライブラリのバージョンなどのフレームワーク ベースのドライバーに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565731" data-raw-source="[&lt;strong&gt;!wdfkd.wdfextendwatchdog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565731)"><strong>!wdfkd.wdfextendwatchdog</strong></a></p></td>
<td align="left"><p>電源遷移中に (10 分 ~ 24 時間) からのフレームワークのウォッチドッグのタイマーのタイムアウト期間を拡張します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565738" data-raw-source="[&lt;strong&gt;!wdfkd.wdffindobjects&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565738)"><strong>!wdfkd.wdffindobjects</strong></a></p></td>
<td align="left"><p>検索し、framework のオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565743" data-raw-source="[&lt;strong&gt;!wdfkd.wdfforwardprogress&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565743)"><strong>!wdfkd.wdfforwardprogress</strong></a></p></td>
<td align="left"><p>に関する情報を表示、<a href="guaranteeing-forward-progress-of-i-o-operations.md" data-raw-source="[guaranteed forward progress](guaranteeing-forward-progress-of-i-o-operations.md)">保証進行</a>の I/O キューの機能です。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565751" data-raw-source="[&lt;strong&gt;!wdfkd.wdfgetdriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565751)"><strong>!wdfkd.wdfgetdriver</strong></a></p></td>
<td align="left"><p>ドライバー名が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565758" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565758)"><strong>!wdfkd.wdfhandle</strong></a></p></td>
<td align="left"><p>Framework のオブジェクト ハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565787" data-raw-source="[&lt;strong&gt;!wdfkd.wdfinterrupt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565787)"><strong>!wdfkd.wdfinterrupt</strong></a></p></td>
<td align="left"><p>フレームワークの割り込みオブジェクト ハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565791" data-raw-source="[&lt;strong&gt;!wdfkd.wdfiotarget&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565791)"><strong>!wdfkd.wdfiotarget</strong></a></p></td>
<td align="left"><p>WDFIOTARGET に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565803" data-raw-source="[&lt;strong&gt;!wdfkd.wdfldr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565803)"><strong>!wdfkd.wdfldr</strong></a></p></td>
<td align="left"><p>すべての framework ライブラリを使用しているドライバーに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565805" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogdump&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565805)"><strong>!wdfkd.wdflogdump</strong></a></p></td>
<td align="left"><p>完全メモリ ダンプ、カーネル メモリ ダンプ、またはライブのカーネル モードの対象から、使用可能な場合、framework のイベント ログのレコードを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566102" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogsave&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566102)"><strong>!wdfkd.wdflogsave</strong></a></p></td>
<td align="left"><p>イベント トレース ログに、フレームワークのイベント ログのレコードを保存します (.<em>etl</em>) を使用して表示できるファイル<a href="https://msdn.microsoft.com/library/windows/hardware/ff553872" data-raw-source="[TraceView](https://msdn.microsoft.com/library/windows/hardware/ff553872)">traceview で</a>します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566103" data-raw-source="[&lt;strong&gt;!wdfkd.wdfmemory&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566103)"><strong>!wdfkd.wdfmemory</strong></a></p></td>
<td align="left"><p>メモリ オブジェクトのバッファーのアドレスとサイズが表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566107" data-raw-source="[&lt;strong&gt;!wdfkd.wdfobject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566107)"><strong>!wdfkd.wdfobject</strong></a></p></td>
<td align="left"><p>Framework のオブジェクトに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566110" data-raw-source="[&lt;strong&gt;!wdfkd.wdfopenhandles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566110)"><strong>!wdfkd.wdfopenhandles</strong></a></p></td>
<td align="left"><p>指定した WDF デバイスで開いているすべてのハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566115" data-raw-source="[&lt;strong&gt;!wdfkd.wdfpoolusage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566115)"><strong>!wdfkd.wdfpoolusage</strong></a></p></td>
<td align="left"><p>ドライバーのメモリ プールの使用率を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566118" data-raw-source="[&lt;strong&gt;!wdfkd.wdfqueue&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566118)"><strong>!wdfkd.wdfqueue</strong></a></p></td>
<td align="left"><p>WDFQUEUE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566119" data-raw-source="[&lt;strong&gt;!wdfkd.wdfrequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566119)"><strong>!wdfkd.wdfrequest</strong></a></p></td>
<td align="left"><p>WDFREQUEST に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566120" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsearchpath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566120)"><strong>!wdfkd.wdfsearchpath</strong></a></p></td>
<td align="left"><p>フレームワークのログの形式のファイルを検索するための検索パスを設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566123" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsettraceprefix&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566123)"><strong>!wdfkd.wdfsettraceprefix</strong></a></p></td>
<td align="left"><p>フレームワークのイベント ログにトレース メッセージのプレフィックス文字列を設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566121" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsetdriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566121)"><strong>!wdfkd.wdfsetdriver</strong></a></p></td>
<td align="left"><p>ドライバー名を必要とするその他のコマンドの既定の名前として使用されるドライバー名を設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566125" data-raw-source="[&lt;strong&gt;!wdfkd.wdfspinlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566125)"><strong>!wdfkd.wdfspinlock</strong></a></p></td>
<td align="left"><p>フレームワークのスピン ロック オブジェクトに関する情報を表示します。 この情報には、スピン ロックの取得の履歴と、ロックが保持されている時間の長さが含まれています。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566126" data-raw-source="[&lt;strong&gt;!wdfkd.wdftagtracker&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566126)"><strong>!wdfkd.wdftagtracker</strong></a></p></td>
<td align="left"><p>指定したオブジェクト タグのタグ情報 (タグの値、行、ファイル、および時間を含む) が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566128" data-raw-source="[&lt;strong&gt;!wdfkd.wdftmffile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566128)"><strong>!wdfkd.wdftmffile</strong></a></p></td>
<td align="left"><p>トレース メッセージの形式を指定します (.<em>tmf</em>) ファイルを<strong>! wdflogdump</strong>拡張機能は、イベント ログのレコードの表示に使用します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566129" data-raw-source="[&lt;strong&gt;!wdfkd.wdftraceprtdebug&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566129)"><strong>!wdfkd.wdftraceprtdebug</strong></a></p></td>
<td align="left"><p>TracePrt 診断モードをオンにします。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265379" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstack&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265379)"><strong>!wdfkd.wdfumdevstack</strong></a></p></td>
<td align="left"><p>詳細については、暗黙的なプロセスで UMDF デバイス スタックを表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265380" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstacks&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265380)"><strong>!wdfkd.wdfumdevstacks</strong></a></p></td>
<td align="left"><p>暗黙的なプロセスですべての UMDF デバイス スタックについての情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265381" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdownirp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265381)"><strong>!wdfkd.wdfumdownirp</strong></a></p></td>
<td align="left"><p>指定されたユーザー モードの IRP に関連付けられているカーネル モード I/O 要求パケット (IRP) が表示されます。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265382" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumfile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265382)"><strong>!wdfkd.wdfumfile</strong></a></p></td>
<td align="left"><p>UMDF のスタック内のファイルに関する情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265383" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265383)"><strong>!wdfkd.wdfumirp</strong></a></p></td>
<td align="left"><p>ユーザー モードの I/O 要求パケット (IRP UM) についての情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265384" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265384)"><strong>!wdfkd.wdfumirps</strong></a></p></td>
<td align="left"><p>暗黙的なプロセスで保留中の I/O 要求パケット (Irp UM) のユーザー モードの一覧を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566131" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbdevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566131)"><strong>!wdfkd.wdfusbdevice</strong></a></p></td>
<td align="left"><p>WDFUSBDEVICE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566134" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbinterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566134)"><strong>!wdfkd.wdfusbinterface</strong></a></p></td>
<td align="left"><p>WDFUSBINTERFACE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566136" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbpipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566136)"><strong>!wdfkd.wdfusbpipe</strong></a></p></td>
<td align="left"><p>WDFUSBPIPE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566137" data-raw-source="[&lt;strong&gt;!wdfkd.wdfwmi&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566137)"><strong>!wdfkd.wdfwmi</strong></a></p></td>
<td align="left"><p>デバイスの Windows Management Instrumentation (WMI) の情報が表示されます。</p></td>
<td align="left">KMDF</td>
</tr>
</tbody>
</table>

 

 

 





