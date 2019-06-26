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
ms.openlocfilehash: a8b04bcffe4ce91bb5b1df6157be714203ad42ab
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393505"
---
#  <a name="summary-of-debugger-extensions-in-wdfkddll"></a>Wdfkd.dll でのデバッガー拡張機能の概要


Windows Driver Kit (WDK) には、という名前のデバッガー拡張機能ライブラリが含まれています。 *Wdfkd.dll*します。 このライブラリには、バージョン 2 以降、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) の両方のドライバーをデバッグに使用できるデバッガー拡張機能のコマンドが含まれています。

各コマンドの詳細については、次を参照してください。 [ **Windows ドライバー フレームワークの拡張機能 (Wdfkd.dll)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)します。 すべての利用可能なデバッガー拡張機能ライブラリの詳細についてで提供されるドキュメントを参照して、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)パッケージ。

KMDF ドライバーでデバッグする方法を示すビデオ シリーズを検索する[ビデオ。KMDF ドライバーのデバッグ](debugging-kernel-mode-driver-framework-drivers.md)します。

UMDF 1.11 またはそれ以前のバージョンを使用するドライバーをデバッグする必要があります代わりに使用する、 *Wudfext.dll*デバッガー拡張機能ライブラリ。 詳細については、次を参照してください。[ユーザー モード ドライバー フレームワークの拡張機能 (Wudfext.dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-extensions--wudfext-dll-)します。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhelp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhelp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhelp)"><strong>!wdfkd.wdfhelp</strong></a></p></td>
<td align="left"><p>このデバッガー拡張機能の一覧が表示されます。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfchildlist" data-raw-source="[&lt;strong&gt;!wdfkd.wdfchildlist&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfchildlist)"><strong>!wdfkd.wdfchildlist</strong></a></p></td>
<td align="left"><p>子リストの状態とすべての子リスト内にあるデバイスの識別の説明に関する情報が表示されます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcollection" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcollection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcollection)"><strong>!wdfkd.wdfcollection</strong></a></p></td>
<td align="left"><p>コレクションに含まれるオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcommonbuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer)"><strong>!wdfkd.wdfcommonbuffer</strong></a></p></td>
<td align="left"><p>に関する情報を表示、<a href="using-common-buffers.md" data-raw-source="[common buffer object](using-common-buffers.md)">共通のバッファー オブジェクト</a>します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcrashdump&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)"><strong>!wdfkd.wdfcrashdump</strong></a></p></td>
<td align="left"><p>小さいメモリ ダンプから、使用可能な場合、framework のイベント ログのレコードを表示します。 フレームワークのイベント ログ レコードがある場合は<a href="registry-values-for-debugging-kmdf-drivers.md" data-raw-source="[ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)">ForceLogsInMiniDump</a>レジストリに設定されている場合、またはフレームワークが、ドライバーにバグ チェックが原因となったことを判断することができます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevext" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevext)"><strong>!wdfkd.wdfdevext</strong></a></p></td>
<td align="left"><p>関連付けられている WDFDEVICE に型指定されたオブジェクトのハンドルが表示されます、 <strong>DeviceExtension</strong>メンバーの Microsoft Windows Driver Model (WDM) <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object" data-raw-source="[&lt;strong&gt;DEVICE_OBJECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)"> <strong>DEVICE_OBJECT</strong> </a>構造体。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)"><strong>!wdfkd.wdfdevice</strong></a></p></td>
<td align="left"><p>WDFDEVICE に型指定されたハンドルに関連付けられている情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdeviceinterrupts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts)"><strong>!wdfkd.wdfdeviceinterrupts</strong></a></p></td>
<td align="left"><p>指定したデバイス ハンドルのすべての割り込みオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevicequeues&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues)"><strong>!wdfkd.wdfdevicequeues</strong></a></p></td>
<td align="left"><p>指定されたデバイスに属するキュー オブジェクトのすべてに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenabler&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)"><strong>!wdfkd.wdfdmaenabler</strong></a></p></td>
<td align="left"><p>に関する情報を表示、 <a href="framework-dma-objects.md" data-raw-source="[DMA enabler object](framework-dma-objects.md)">DMA イネーブラー オブジェクト</a>、およびその関連付けられた DMA トランザクション オブジェクトと共通のバッファー オブジェクト。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenablers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers)"><strong>!wdfkd.wdfdmaenablers</strong></a></p></td>
<td align="left"><p>すべての DMA イネーブラー オブジェクト、DMA トランザクション オブジェクト、および指定したデバイス オブジェクトに関連付けられている共通のバッファー オブジェクトの概要を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmatransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)"><strong>!wdfkd.wdfdmatransaction</strong></a></p></td>
<td align="left"><p>WDF ダイレクト メモリ アクセス (DMA) トランザクション オブジェクトについての情報を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdriverinfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)"><strong>!wdfkd.wdfdriverinfo</strong></a></p></td>
<td align="left"><p>オブジェクトのハンドルの階層を変更したライブラリのバージョンなどのフレームワーク ベースのドライバーに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfextendwatchdog" data-raw-source="[&lt;strong&gt;!wdfkd.wdfextendwatchdog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfextendwatchdog)"><strong>!wdfkd.wdfextendwatchdog</strong></a></p></td>
<td align="left"><p>電源遷移中に (10 分 ~ 24 時間) からのフレームワークのウォッチドッグのタイマーのタイムアウト期間を拡張します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdffindobjects" data-raw-source="[&lt;strong&gt;!wdfkd.wdffindobjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdffindobjects)"><strong>!wdfkd.wdffindobjects</strong></a></p></td>
<td align="left"><p>検索し、framework のオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfforwardprogress" data-raw-source="[&lt;strong&gt;!wdfkd.wdfforwardprogress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfforwardprogress)"><strong>!wdfkd.wdfforwardprogress</strong></a></p></td>
<td align="left"><p>に関する情報を表示、<a href="guaranteeing-forward-progress-of-i-o-operations.md" data-raw-source="[guaranteed forward progress](guaranteeing-forward-progress-of-i-o-operations.md)">保証進行</a>の I/O キューの機能です。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfgetdriver" data-raw-source="[&lt;strong&gt;!wdfkd.wdfgetdriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfgetdriver)"><strong>!wdfkd.wdfgetdriver</strong></a></p></td>
<td align="left"><p>ドライバー名が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhandle" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhandle)"><strong>!wdfkd.wdfhandle</strong></a></p></td>
<td align="left"><p>Framework のオブジェクト ハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt" data-raw-source="[&lt;strong&gt;!wdfkd.wdfinterrupt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt)"><strong>!wdfkd.wdfinterrupt</strong></a></p></td>
<td align="left"><p>フレームワークの割り込みオブジェクト ハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfiotarget" data-raw-source="[&lt;strong&gt;!wdfkd.wdfiotarget&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfiotarget)"><strong>!wdfkd.wdfiotarget</strong></a></p></td>
<td align="left"><p>WDFIOTARGET に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr" data-raw-source="[&lt;strong&gt;!wdfkd.wdfldr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)"><strong>!wdfkd.wdfldr</strong></a></p></td>
<td align="left"><p>すべての framework ライブラリを使用しているドライバーに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogdump&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)"><strong>!wdfkd.wdflogdump</strong></a></p></td>
<td align="left"><p>完全メモリ ダンプ、カーネル メモリ ダンプ、またはライブのカーネル モードの対象から、使用可能な場合、framework のイベント ログのレコードを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogsave" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogsave&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogsave)"><strong>!wdfkd.wdflogsave</strong></a></p></td>
<td align="left"><p>イベント トレース ログに、フレームワークのイベント ログのレコードを保存します (.<em>etl</em>) を使用して表示できるファイル<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview" data-raw-source="[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)">traceview で</a>します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfmemory" data-raw-source="[&lt;strong&gt;!wdfkd.wdfmemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfmemory)"><strong>!wdfkd.wdfmemory</strong></a></p></td>
<td align="left"><p>メモリ オブジェクトのバッファーのアドレスとサイズが表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfobject" data-raw-source="[&lt;strong&gt;!wdfkd.wdfobject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfobject)"><strong>!wdfkd.wdfobject</strong></a></p></td>
<td align="left"><p>Framework のオブジェクトに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfopenhandles" data-raw-source="[&lt;strong&gt;!wdfkd.wdfopenhandles&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfopenhandles)"><strong>!wdfkd.wdfopenhandles</strong></a></p></td>
<td align="left"><p>指定した WDF デバイスで開いているすべてのハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfpoolusage" data-raw-source="[&lt;strong&gt;!wdfkd.wdfpoolusage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfpoolusage)"><strong>!wdfkd.wdfpoolusage</strong></a></p></td>
<td align="left"><p>ドライバーのメモリ プールの使用率を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfqueue" data-raw-source="[&lt;strong&gt;!wdfkd.wdfqueue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfqueue)"><strong>!wdfkd.wdfqueue</strong></a></p></td>
<td align="left"><p>WDFQUEUE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfrequest" data-raw-source="[&lt;strong&gt;!wdfkd.wdfrequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfrequest)"><strong>!wdfkd.wdfrequest</strong></a></p></td>
<td align="left"><p>WDFREQUEST に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsearchpath" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsearchpath&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsearchpath)"><strong>!wdfkd.wdfsearchpath</strong></a></p></td>
<td align="left"><p>フレームワークのログの形式のファイルを検索するための検索パスを設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsettraceprefix" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsettraceprefix&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsettraceprefix)"><strong>!wdfkd.wdfsettraceprefix</strong></a></p></td>
<td align="left"><p>フレームワークのイベント ログにトレース メッセージのプレフィックス文字列を設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsetdriver" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsetdriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsetdriver)"><strong>!wdfkd.wdfsetdriver</strong></a></p></td>
<td align="left"><p>ドライバー名を必要とするその他のコマンドの既定の名前として使用されるドライバー名を設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfspinlock" data-raw-source="[&lt;strong&gt;!wdfkd.wdfspinlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfspinlock)"><strong>!wdfkd.wdfspinlock</strong></a></p></td>
<td align="left"><p>フレームワークのスピン ロック オブジェクトに関する情報を表示します。 この情報には、スピン ロックの取得の履歴と、ロックが保持されている時間の長さが含まれています。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker" data-raw-source="[&lt;strong&gt;!wdfkd.wdftagtracker&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)"><strong>!wdfkd.wdftagtracker</strong></a></p></td>
<td align="left"><p>指定したオブジェクト タグのタグ情報 (タグの値、行、ファイル、および時間を含む) が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftmffile" data-raw-source="[&lt;strong&gt;!wdfkd.wdftmffile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftmffile)"><strong>!wdfkd.wdftmffile</strong></a></p></td>
<td align="left"><p>トレース メッセージの形式を指定します (.<em>tmf</em>) ファイルを<strong>! wdflogdump</strong>拡張機能は、イベント ログのレコードの表示に使用します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftraceprtdebug" data-raw-source="[&lt;strong&gt;!wdfkd.wdftraceprtdebug&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftraceprtdebug)"><strong>!wdfkd.wdftraceprtdebug</strong></a></p></td>
<td align="left"><p>TracePrt 診断モードをオンにします。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)"><strong>!wdfkd.wdfumdevstack</strong></a></p></td>
<td align="left"><p>詳細については、暗黙的なプロセスで UMDF デバイス スタックを表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstacks&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)"><strong>!wdfkd.wdfumdevstacks</strong></a></p></td>
<td align="left"><p>暗黙的なプロセスですべての UMDF デバイス スタックについての情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdownirp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp)"><strong>!wdfkd.wdfumdownirp</strong></a></p></td>
<td align="left"><p>指定されたユーザー モードの IRP に関連付けられているカーネル モード I/O 要求パケット (IRP) が表示されます。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)"><strong>!wdfkd.wdfumfile</strong></a></p></td>
<td align="left"><p>UMDF のスタック内のファイルに関する情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)"><strong>!wdfkd.wdfumirp</strong></a></p></td>
<td align="left"><p>ユーザー モードの I/O 要求パケット (IRP UM) についての情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)"><strong>!wdfkd.wdfumirps</strong></a></p></td>
<td align="left"><p>暗黙的なプロセスで保留中の I/O 要求パケット (Irp UM) のユーザー モードの一覧を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbdevice" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbdevice)"><strong>!wdfkd.wdfusbdevice</strong></a></p></td>
<td align="left"><p>WDFUSBDEVICE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbinterface" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbinterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbinterface)"><strong>!wdfkd.wdfusbinterface</strong></a></p></td>
<td align="left"><p>WDFUSBINTERFACE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbpipe" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbpipe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbpipe)"><strong>!wdfkd.wdfusbpipe</strong></a></p></td>
<td align="left"><p>WDFUSBPIPE に型指定されたオブジェクトのハンドルに関する情報が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfwmi" data-raw-source="[&lt;strong&gt;!wdfkd.wdfwmi&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfwmi)"><strong>!wdfkd.wdfwmi</strong></a></p></td>
<td align="left"><p>デバイスの Windows Management Instrumentation (WMI) の情報が表示されます。</p></td>
<td align="left">KMDF</td>
</tr>
</tbody>
</table>

 

 

 





