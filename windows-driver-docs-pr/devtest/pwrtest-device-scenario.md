---
title: PwrTest のデバイス シナリオ
description: PwrTest Device シナリオでは、デバイスのアイドル状態の統計を監視します。
ms.assetid: 75C53B6E-3D1F-4E9D-A99E-3060A9CC37BC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea350821f85cba2f100b88a27d0ff30e88d9171b
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769664"
---
# <a name="pwrtest-device-scenario"></a>PwrTest のデバイス シナリオ


PwrTest Device シナリオでは、デバイスのアイドル状態の統計を監視します。

このシナリオは、主に Windows 7 デバイスの電源動作で使用されます。それ以降のバージョンの Windows では、Pwrtest で現在サポートされていないデバイスのアイドル状態を追跡するための別のメカニズムを使用します。 Windows 7 より新しいバージョンの Windows では、 [Windows パフォーマンスツールキット (WPT)](https://docs.microsoft.com/windows-hardware/test/wpt/windows-performance-toolkit-technical-reference)を使用します。 WPT には、Windows パフォーマンスレコーダー (WPR) が含まれています。このツールを使用すると、カーネルモードの電源プロバイダーと、power framework (PoFx) デバイスの統計情報を表示できる windows performance Analyzer (WPA) をトレースし、後で移行をグラフ化できます。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


```
pwrtest /device  [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
シナリオが実行されるまでの合計時間 (分) を指定します ( *n*の既定値は30分です)。

**例**

```
pwrtest /device /t:60
```

```
pwrtest /device
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <DeviceIdleEvents> 
    <DeviceIdleChangeEvent>
        <Timestamp></TimeStamp>
        <InstancePath></InstancePath>
        <Description></Description>
    </DeviceIdleChangeEvent>
    <DeviceIdleEvent>
        <Timestamp></TimeStamp>
        <InstancePath></InstancePath>
        <Device></Device>
        <Pdo></Pdo>
        <ConservationTimeout></ConservationTimeout>
        <PerformanceTimeout></PerformanceTimeout>
        <AccruedIdleTime></AccruedIdleTime>
        <BusyCount></BusyCount>
        <AccruedBusyCount></AccruedBusyCount>
        <IdlePowerState></IdlePowerState>
        <CurrentPowerState></CurrentPowerState>
        <Analysis></Analysis>
    </DeviceIdleEvent>
  </DeviceIdleEvents>
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
<td align="left"><strong>&lt;DeviceIdleEvents&gt;</strong></td>
<td align="left"><p>さまざまなデバイスのアイドル状態のイベントがすべて含まれます。 PwrTest ログファイルあたり1つの<strong> &lt; DeviceIdleEvents</strong>要素のみです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InstancePath&gt;</strong></td>
<td align="left"><p>デバイスインスタンスパス。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DeviceIdleChangeEvent&gt;</strong></td>
<td align="left"><p>デバイスの追加または削除イベント。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;説明&gt;</strong></td>
<td align="left"><p>DeviceRemoved または DeviceDetected 検出されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DeviceIdleEvent&gt;</strong></td>
<td align="left"><p>デバイスのアイドル状態の統計イベント。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;デバイス&gt;</strong></td>
<td align="left"><p>機能デバイスオブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Pdo&gt;</strong></td>
<td align="left"><p>物理デバイスオブジェクト</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ConservationTimeout&gt;</strong></td>
<td align="left"><p>控えめタイムアウト (通常は DC 電源で使用されます)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;パフォーマンスタイムアウト&gt;</strong></td>
<td align="left"><p>パフォーマンスのタイムアウト (通常は AC 電源で使用されます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>期間中に発生したアイドル時間。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BusyCount&gt;</strong></td>
<td align="left"><p>デバイスドライバーが期間中に<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>Posetdevicebusy</strong></a>を呼び出した回数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedBusyCount&gt;</strong></td>
<td align="left"><p>デバイスドライバーが<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer" data-raw-source="[&lt;strong&gt;PoSetDeviceBusy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)"><strong>Posetdevicebusy</strong></a>を呼び出した合計回数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdlePowerState&gt;</strong></td>
<td align="left"><p>アイドル状態になっている数値の状態を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentPowerState&gt;</strong></td>
<td align="left"><p>現在の数値の電源の状態。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;分析&gt;</strong></td>
<td align="left"><p>期間中に発生した処理を説明する文字列。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest の構文](pwrtest-syntax.md)










