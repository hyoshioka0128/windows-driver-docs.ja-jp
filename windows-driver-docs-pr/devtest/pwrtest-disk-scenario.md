---
title: PwrTest のディスク シナリオ
description: PwrTest Disk シナリオでは、ディスクのアイドル状態の統計とスピンダウンイベントを監視します。
ms.assetid: E54AA721-27C6-4E42-B42A-77AC70711A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ea0a51f226a0a13a5577c2e78fab12aa3525c4f
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769662"
---
# <a name="pwrtest-disk-scenario"></a>PwrTest のディスク シナリオ


PwrTest Disk シナリオでは、ディスクのアイドル状態の統計とスピンダウンイベントを監視します。

このシナリオは、主に Windows 7 のハードディスクの電源動作で使用されます。それ以降のバージョンの Windows では、Pwrtest で現在サポートされていないディスクのアイドル状態を追跡するための別のメカニズムを使用します。 Windows 7 より新しいバージョンの Windows では、 [Windows パフォーマンスツールキット (WPT)](https://docs.microsoft.com/windows-hardware/test/wpt/windows-performance-toolkit-technical-reference)を使用します。 WPT には、Windows パフォーマンスレコーダー (WPR) が含まれています。このツールを使用すると、カーネルモードの電源プロバイダーと、power framework (PoFx) デバイスの統計情報を表示できる windows performance Analyzer (WPA) をトレースし、後で移行をグラフ化できます。

**メモ**   このシナリオは、すべての記憶域ドライバーがアイドル検出に登録するわけではないため、すべての種類のディスクまたはコントローラーでは機能しません。 詳細については[、「ストレージクラスドライバーでの PnP 開始の処理](https://docs.microsoft.com/windows-hardware/drivers/storage/handling-pnp-start-in-a-storage-class-driver)」を参照してください。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


```
pwrtest /disk  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
シナリオが実行されるまでの合計時間 (分) を指定します ( *n*の既定値は30分です)。

**例**

```
pwrtest /disk /t:60
```

```
pwrtest /disk
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <DiskIdleEvents> 
    <DiskIdleChangeEvent>
        <Timestamp></TimeStamp>
        <DiskNumber></DiskNumber>
        <InstancePath></InstancePath>
        <Description></Description>
    </DiskIdleChangeEvent>
    <DiskIdlePolicyChange>
        <Timestamp></TimeStamp>
        <Timeout></Timeout>
        <IgnoreThreshold></IgnoreThreshold>
    </DiskIdlePolicyChange>
    <DiskIdleEvent>
        <Timestamp></TimeStamp>
        <DiskNumber></DiskNumber>
        <InstancePath></InstancePath>
        <Device></Device>
        <Pdo></Pdo>
        <BusyCount></BusyCount>
        <AccruedBusyCount></AccruedBusyCount>
        <IdlePowerState></IdlePowerState>
        <CurrentPowerState></CurrentPowerState>
        <Timeout></Timeout>
        <IgnoreThreshold></IgnoreThreshold>
        <AccruedIdleTime></AccruedIdleTime>
        <AccruedNonIdleTime></AccruedNonIdleTime>
        <Analysis></Analysis>
    </DiskIdleEvent>
  </DiskIdleEvents>
</PwrTestLog> 
```

次の表では、ログファイルに表示される XML 要素について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要素</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>&lt;DiskIdleEvents&gt;</strong></td>
<td align="left"><p>すべてのディスクアイドルイベントを格納します。 &lt; &gt; PwrTest ログファイルあたり1つの DeviceIdleEvents 要素のみです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskNumber&gt;</strong></td>
<td align="left"><p>このイベントが発生している物理ディスクを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;InstancePath&gt;</strong></td>
<td align="left"><p>デバイスインスタンスパス。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DeviceIdleChangeEvent&gt;</strong></td>
<td align="left"><p>デバイスの追加または削除イベント。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;説明&gt;</strong></td>
<td align="left"><p>DeviceRemoved または DeviceDetected 検出されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskIdlePolicyChange&gt;</strong></td>
<td align="left"><p>ディスクのタイムアウト変更イベント。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムアウト&gt;</strong></td>
<td align="left"><p>新しいディスクのスピンダウンタイムアウト。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>新しいディスクのアイドル状態を無視するしきい値。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;デバイス&gt;</strong></td>
<td align="left"><p>機能デバイスオブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理デバイスオブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>デバイスドライバーが期間中に<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>Posetdevicebusy</strong></a>を呼び出した回数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>デバイスドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>Posetdevicebusy</strong></a>の合計を呼び出す回数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>アイドル状態の状態を表す数値。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>現在の数値の電源の状態。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムアウト&gt;</strong></td>
<td align="left"><p>タイムアウト (秒)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>非アイドル時間が無視される秒数</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>期間中の未収アイドル時間。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedNonIdleTime&gt;</strong></td>
<td align="left"><p>見越計上されたアイドル時間の合計。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>期間中に発生した処理を説明する文字列。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest の構文](pwrtest-syntax.md)

 

 






