---
title: PwrTest のディスクのシナリオ
description: PwrTest のディスクのシナリオでは、ディスクのアイドル状態の統計およびスピン ダウン イベントを監視します。
ms.assetid: E54AA721-27C6-4E42-B42A-77AC70711A26
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 671cee3e73d0a0a64a8efbf4a4c2cea17cd1d265
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535336"
---
# <a name="pwrtest-disk-scenario"></a>PwrTest のディスクのシナリオ


PwrTest のディスクのシナリオでは、ディスクのアイドル状態の統計およびスピン ダウン イベントを監視します。

このシナリオは、主に Windows 7 のハード_ディスクの電源の動作の使用、Windows の今後のバージョンが Pwrtest で現在サポートされていないディスクをアイドル状態を追跡するため、別のメカニズムを使用します。 Windows 7 よりも新しい Windows のバージョン、使用、 [Windows パフォーマンス ツールキット (WPT)](https://go.microsoft.com/fwlink/p/?linkid=294280)します。 WPT には、カーネル モードの電源プロバイダーをトレースするために使用できる Windows Performance Recorder (WPR) と Windows パフォーマンス アナライザー (WPA) フレームワーク (PoFx) デバイスの電源の統計を表示することができますし、その後、遷移グラフ化できますが含まれています。

**注**  このシナリオでは、アイドル状態検出のすべての記憶装置ドライバーを登録するため、すべての種類のディスクまたはコント ローラー機能しません。 参照してください[、記憶域クラス ドライバーの PnP 開始を処理](https://msdn.microsoft.com/library/windows/hardware/ff554995)詳細についてはします。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /disk  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

**例**

```
pwrtest /disk /t:60
```

```
pwrtest /disk
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

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

次の表では、ログ ファイルに表示される XML 要素について説明します。

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
<td align="left"><p>すべての別のディスク アイドル イベントが含まれています。 1 つだけ&lt;DeviceIdleEvents&gt; PwrTest ログ ファイルごとの要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskNumber&gt;</strong></td>
<td align="left"><p>物理ディスクは、このイベントを識別するためです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;InstancePath&gt;</strong></td>
<td align="left"><p>デバイス インスタンスのパス。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DeviceIdleChangeEvent&gt;</strong></td>
<td align="left"><p>デバイスでは、追加またはイベントを削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;説明&gt;</strong></td>
<td align="left"><p>DeviceRemoved または DeviceDetected します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DiskIdlePolicyChange&gt;</strong></td>
<td align="left"><p>ディスクのタイムアウトは、イベントを変更します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムアウト&gt;</strong></td>
<td align="left"><p>新しいディスク スピン ダウンがタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>新しいディスクのアイドル状態では、しきい値を無視します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;デバイス&gt;</strong></td>
<td align="left"><p>機能のデバイス オブジェクト。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理デバイス オブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>デバイス ドライバーが呼び出された回数<a href="https://msdn.microsoft.com/library/windows/hardware/ff559755" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559755)"> <strong>PoSetDeviceBusy</strong> </a>期間中にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>デバイス ドライバーの呼び出しがタイムアウト数<a href="https://msdn.microsoft.com/library/windows/hardware/ff559755" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559755)"> <strong>PoSetDeviceBusy</strong> </a>合計します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>どのような数値の状態は、アイドル状態です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>現在の数値の電源の状態。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムアウト&gt;</strong></td>
<td align="left"><p>タイムアウト (秒単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IgnoreThreshold&gt;</strong></td>
<td align="left"><p>無視する非アイドル時間の秒数</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>期間中に未収のアイドル時間。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedNonIdleTime&gt;</strong></td>
<td align="left"><p>発生する総アイドル時間。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>期間中の変更点を説明する文字列。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






