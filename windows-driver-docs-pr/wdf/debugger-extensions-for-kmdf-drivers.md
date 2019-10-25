---
title: Wdfkd.dll でのデバッガー拡張機能の概要
description: Windows Driver Kit (WDK) には、Wdfkd .dll という名前のデバッガー拡張ライブラリが含まれています。
ms.assetid: 5a83ea58-5dbf-40a6-b4cb-9c330851fc33
keywords:
- 拡張機能の WDK デバッガー
- デバッガー拡張機能 (WDK KMDF)
- デバッグドライバー WDK KMDF、デバッガー拡張機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f0b5937e06a60baf24d98735cd9d47c2e031bb4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844671"
---
#  <a name="summary-of-debugger-extensions-in-wdfkddll"></a>Wdfkd.dll でのデバッガー拡張機能の概要


Windows Driver Kit (WDK) には、 *Wdfkd .dll*という名前のデバッガー拡張ライブラリが含まれています。 このライブラリには、バージョン2以降のカーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) ドライバーの両方をデバッグするために使用できるデバッガー拡張コマンドが含まれています。

各コマンドの詳細については、「 [**Windows Driver Framework Extensions (Wdfkd .dll)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)」を参照してください。 使用可能なすべてのデバッガー拡張機能ライブラリの詳細については、 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)パッケージに付属のドキュメントを参照してください。

KMDF ドライバーのデバッグ方法を示すビデオシリーズについては、 [「ビデオ: KMDF ドライバーのデバッグ](debugging-kernel-mode-driver-framework-drivers.md)」を参照してください。

UMDF version 1.11 以前を使用しているドライバーをデバッグするには、代わりに*Wudfext*デバッガー拡張機能ライブラリを使用する必要があります。 詳細については、「[ユーザーモードドライバーフレームワークの拡張機能 (Wudfext .dll)](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-extensions--wudfext-dll-)」を参照してください。

*Wdfkd*拡張子ライブラリに用意されている拡張コマンドには、次のものがあります。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhelp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhelp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhelp)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>このデバッガー拡張機能の一覧を表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfchildlist" data-raw-source="[&lt;strong&gt;!wdfkd.wdfchildlist&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfchildlist)"><strong>! wdfkd. wdfchildlist</strong></a></p></td>
<td align="left"><p>子リストの状態と、子リストにあるすべてのデバイス id の説明に関する情報が表示されます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcollection" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcollection&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcollection)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>コレクションに含まれるオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcommonbuffer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcommonbuffer)"><strong>! wdfkd. wdfcommonbuffer</strong></a></p></td>
<td align="left"><p><a href="using-common-buffers.md" data-raw-source="[common buffer object](using-common-buffers.md)">共通のバッファーオブジェクト</a>に関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump" data-raw-source="[&lt;strong&gt;!wdfkd.wdfcrashdump&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)"><strong>! wdfkd。 wdfkd</strong></a></p></td>
<td align="left"><p>使用可能な場合は、フレームワークのイベントログレコードを小さいメモリダンプから表示します。 レジストリに<a href="registry-values-for-debugging-kmdf-drivers.md" data-raw-source="[ForceLogsInMiniDump](registry-values-for-debugging-kmdf-drivers.md)">Forcelogsinminidump ダンプ</a>が設定されている場合、または、ドライバーによってバグチェックが発生したことをフレームワークが判断できる場合は、フレームワークのイベントログレコードを使用できます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevext" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevext)"><strong>! wdfkd。 wdfdevext</strong></a></p></td>
<td align="left"><p>Microsoft Windows Driver Model (WDM) <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object" data-raw-source="[&lt;strong&gt;DEVICE_OBJECT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)"><strong>DEVICE_OBJECT</strong></a>構造体の<strong>deviceextension</strong>メンバーに関連付けられている、wdfdevice 型のオブジェクトハンドルを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)"><strong>! wdfkd wdfkd</strong></a></p></td>
<td align="left"><p>WDFDEVICE 型のハンドルに関連付けられている情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdeviceinterrupts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdeviceinterrupts)"><strong>! wdfkd. wdfdevice割込み</strong></a></p></td>
<td align="left"><p>指定したデバイスハンドルのすべての割り込みオブジェクトを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdevicequeues&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues)"><strong>! wdfkd キュー</strong></a></p></td>
<td align="left"><p>指定したデバイスに属するすべてのキューオブジェクトに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenabler&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenabler)"><strong>! wdfkd. wdfdmaenabler</strong></a></p></td>
<td align="left"><p><a href="framework-dma-objects.md" data-raw-source="[DMA enabler object](framework-dma-objects.md)">Dma イネーブラーオブジェクト</a>と、それに関連付けられている dma トランザクションオブジェクトおよび共通のバッファーオブジェクトに関する情報を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmaenablers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmaenablers)"><strong>! wdfkd. wdfdmaenabler</strong></a></p></td>
<td align="left"><p>指定したデバイスオブジェクトに関連付けられているすべての DMA イネーブラーオブジェクト、DMA トランザクションオブジェクト、および共通バッファーオブジェクトの概要が表示されます。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdmatransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdmatransaction)"><strong>! wdfkd. wdfdmatransaction</strong></a></p></td>
<td align="left"><p>WDF ダイレクトメモリアクセス (DMA) トランザクションオブジェクトに関する情報を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo" data-raw-source="[&lt;strong&gt;!wdfkd.wdfdriverinfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo)"><strong>! wdfkd. wdfdriverinfo</strong></a></p></td>
<td align="left"><p>ライブラリのバージョンやオブジェクトハンドルの階層など、フレームワークベースのドライバーに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfextendwatchdog" data-raw-source="[&lt;strong&gt;!wdfkd.wdfextendwatchdog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfextendwatchdog)"><strong>! wdfkd. wdfextendwatchdog</strong></a></p></td>
<td align="left"><p>電源遷移中に、フレームワークのウォッチドッグタイマーのタイムアウト時間 (10 分から24時間) を延長します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdffindobjects" data-raw-source="[&lt;strong&gt;!wdfkd.wdffindobjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdffindobjects)"><strong>! wdfkd。 wdffindoobjects</strong></a></p></td>
<td align="left"><p>フレームワークオブジェクトを検索して表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfforwardprogress" data-raw-source="[&lt;strong&gt;!wdfkd.wdfforwardprogress&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfforwardprogress)"><strong>! wdfkd. wdfforwardprogress</strong></a></p></td>
<td align="left"><p>I/o キューの保証された<a href="guaranteeing-forward-progress-of-i-o-operations.md" data-raw-source="[guaranteed forward progress](guaranteeing-forward-progress-of-i-o-operations.md)">事前進行</a>の機能に関する情報を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfgetdriver" data-raw-source="[&lt;strong&gt;!wdfkd.wdfgetdriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfgetdriver)"><strong>! wdfkd. wdfgetdriver</strong></a></p></td>
<td align="left"><p>ドライバー名が表示されます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhandle" data-raw-source="[&lt;strong&gt;!wdfkd.wdfhandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfhandle)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>フレームワークオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt" data-raw-source="[&lt;strong&gt;!wdfkd.wdfinterrupt&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfinterrupt)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>フレームワークの割り込みオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfiotarget" data-raw-source="[&lt;strong&gt;!wdfkd.wdfiotarget&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfiotarget)"><strong>! wdfkd. wdfiotarget</strong></a></p></td>
<td align="left"><p>WDFIOTARGET 型のオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr" data-raw-source="[&lt;strong&gt;!wdfkd.wdfldr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)"><strong>! wdfkd. wdfldr</strong></a></p></td>
<td align="left"><p>フレームワークライブラリを使用しているすべてのドライバーに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 1</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogdump&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)"><strong>! wdfkd. wdflogdump</strong></a></p></td>
<td align="left"><p>フレームワークのイベントログレコードを表示します (使用可能な場合)。完全なメモリダンプ、カーネルメモリダンプ、またはライブカーネルモードターゲットを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogsave" data-raw-source="[&lt;strong&gt;!wdfkd.wdflogsave&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogsave)"><strong>! wdfkd. wdflogsave</strong></a></p></td>
<td align="left"><p>フレームワークのイベントログレコードをイベントトレースログ () に保存します。<em>etl</em>) ファイルは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview" data-raw-source="[TraceView](https://docs.microsoft.com/windows-hardware/drivers/devtest/traceview)">traceview</a>を使用して表示できます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfmemory" data-raw-source="[&lt;strong&gt;!wdfkd.wdfmemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfmemory)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>メモリオブジェクトのバッファーアドレスとサイズを表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfobject" data-raw-source="[&lt;strong&gt;!wdfkd.wdfobject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfobject)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>フレームワークオブジェクトに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfopenhandles" data-raw-source="[&lt;strong&gt;!wdfkd.wdfopenhandles&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfopenhandles)"><strong>! wdfkd. wdfopenhandle</strong></a></p></td>
<td align="left"><p>指定された WDF デバイスで開いているすべてのハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfpoolusage" data-raw-source="[&lt;strong&gt;!wdfkd.wdfpoolusage&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfpoolusage)"><strong>! wdfkd. wdfpoolusage</strong></a></p></td>
<td align="left"><p>ドライバーのメモリプール使用率を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfqueue" data-raw-source="[&lt;strong&gt;!wdfkd.wdfqueue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfqueue)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>WDFQUEUE 型のオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfrequest" data-raw-source="[&lt;strong&gt;!wdfkd.wdfrequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfrequest)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>WDFREQUEST 型のオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsearchpath" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsearchpath&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsearchpath)"><strong>! wdfkd. wdfsearchpath</strong></a></p></td>
<td align="left"><p>フレームワークログのフォーマットファイルを検索するための検索パスを設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsettraceprefix" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsettraceprefix&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsettraceprefix)"><strong>! wdfkd。 wdfsettraceprefix</strong></a></p></td>
<td align="left"><p>フレームワークのイベントログ内のトレースメッセージのプレフィックス文字列を設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsetdriver" data-raw-source="[&lt;strong&gt;!wdfkd.wdfsetdriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfsetdriver)"><strong>! wdfkd. wdfsetdriver</strong></a></p></td>
<td align="left"><p>ドライバー名を必要とする他のコマンドの既定の名前として使用されるドライバー名を設定します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfspinlock" data-raw-source="[&lt;strong&gt;!wdfkd.wdfspinlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfspinlock)"><strong>! wdfkd. wdfkd ロック</strong></a></p></td>
<td align="left"><p>フレームワークのスピンロックオブジェクトに関する情報を表示します。 この情報には、スピンロックの取得履歴と、ロックが保持されていた時間の長さが含まれます。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker" data-raw-source="[&lt;strong&gt;!wdfkd.wdftagtracker&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftagtracker)"><strong>! wdfkd. wdftagtracker</strong></a></p></td>
<td align="left"><p>指定されたオブジェクトタグのタグ情報 (タグ値、行、ファイル、時刻を含む) を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftmffile" data-raw-source="[&lt;strong&gt;!wdfkd.wdftmffile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftmffile)"><strong>! wdfkd. wdftmffile</strong></a></p></td>
<td align="left"><p>トレースメッセージの形式 () を指定します。<em>tmf</em>) <strong>! wdflogdump</strong>拡張機能がイベントログレコードを表示するために使用するファイル。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftraceprtdebug" data-raw-source="[&lt;strong&gt;!wdfkd.wdftraceprtdebug&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdftraceprtdebug)"><strong>! wdfkd. wdftraceprtdebug</strong></a></p></td>
<td align="left"><p>TracePrt 診断モードをオンにします。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstack)"><strong>! wdfkd. wdfumdevstack</strong></a></p></td>
<td align="left"><p>暗黙のプロセスでの UMDF デバイススタックに関する詳細情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdevstacks&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdevstacks)"><strong>! wdfkd. wdfumdevstacks</strong></a></p></td>
<td align="left"><p>暗黙的なプロセス内のすべての UMDF デバイススタックに関する情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumdownirp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumdownirp)"><strong>! wdfkd. wdfumdownirp</strong></a></p></td>
<td align="left"><p>指定されたユーザーモードの IRP に関連付けられているカーネルモード i/o 要求パケット (IRP) を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumfile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumfile)"><strong>! wdfkd. wdfumfile</strong></a></p></td>
<td align="left"><p>UMDF のスタック内のファイルに関する情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirp)"><strong>! wdfkd. wdfumirp</strong></a></p></td>
<td align="left"><p>ユーザーモード i/o 要求パケット (UM IRP) に関する情報を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps" data-raw-source="[&lt;strong&gt;!wdfkd.wdfumirps&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)"><strong>! wdfkd. wdfumirps</strong></a></p></td>
<td align="left"><p>暗黙のプロセスで保留中のユーザーモード i/o 要求パケット (UM Irp) の一覧を表示します。</p></td>
<td align="left"><p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbdevice" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbdevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbdevice)"><strong>! wdfkd. wdfusbdevice</strong></a></p></td>
<td align="left"><p>WDFUSBDEVICE によって型指定されたオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbinterface" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbinterface&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbinterface)"><strong>! wdfkd. wdfusbinterface</strong></a></p></td>
<td align="left"><p>WDFUSBINTERFACE によって型指定されたオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbpipe" data-raw-source="[&lt;strong&gt;!wdfkd.wdfusbpipe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfusbpipe)"><strong>! wdfkd. wdfusbpipe</strong></a></p></td>
<td align="left"><p>WDFUSBPIPE によって型指定されたオブジェクトハンドルに関する情報を表示します。</p></td>
<td align="left"><p>KMDF</p>
<p>UMDF 2</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfwmi" data-raw-source="[&lt;strong&gt;!wdfkd.wdfwmi&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfwmi)"><strong>! wdfkd. wdfkd</strong></a></p></td>
<td align="left"><p>デバイスの Windows Management Instrumentation (WMI) 情報を表示します。</p></td>
<td align="left">KMDF</td>
</tr>
</tbody>
</table>

 

 

 





