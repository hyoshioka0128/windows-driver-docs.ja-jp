---
title: PwrTest の温度シナリオ
description: PwrTest Thermal シナリオでは、ACPI の温度ゾーン情報と統計情報を監視します。
ms.assetid: C6941A50-EA0F-4C46-A290-8CAAD292E156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3d9e86da55a505ad8dd6835e15d32a8ad3a4347
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769572"
---
# <a name="pwrtest-thermal-scenario"></a>PwrTest の温度シナリオ


PwrTest Thermal シナリオでは、ACPI の温度ゾーン情報と統計情報を監視します。 このシナリオは、サーマルゾーンと温度の変化を報告するシステムでのみサポートされています。

**メモ** このシナリオは、オペレーティングシステムに対して温度データを報告するシステムでのみ機能します。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


```
pwrtest /thermal [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
シナリオが実行されるまでの合計時間 (分) を指定します ( *n*の既定値は30分です)。

<span id="_temp_kcf"></span><span id="_TEMP_KCF"></span>**/一時:**{**k** | **c** | **f**}  
すべての出力とログに使用する気温 (**k**)、摂氏 (**c**)、華氏 (**f**) を指定します (既定値はケルビン)。

**例**

```
pwrtest /thermal  
```

```
pwrtest /thermal  /t:30
```

```
pwrtest /thermal  /t:30 /temp:f
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <ThermalEvents> 
    <PassiveCooling>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_TMP></_TMP>
        <_PSV></_PSV>
        <_TC1></_TC1>
        <_TC2></_TC2>
        <_TSP></_TSP>
    </PassiveCooling>
    <ActiveCooling>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_TMP></_TMP>
        <_AC0></_AC0>
        <_AC1></_AC1>
        <_AC2></_AC2>
        <_AC3></_AC3>
        <_AC4></_AC4>
        <_AC5></_AC5>
        <_AC6></_AC6>
        <_AC7></_AC7>
        <_AC8></_AC8>
        <_AC9></_AC9>
    </ActiveCooling>
    <Hot>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_HOT></_HOT>
    </Hot>
    <Critical>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <_CRT></_CRT>
    </Critical>
    <ActiveCoolingDevicePower>
        <Timestamp></TimeStamp>
        <TemperatureScale></TemperatureScale>
        <ThermalZoneDeviceInstance></ThermalZoneDeviceInstance>
        <FanDeviceInstance></FanDeviceInstance>
        <PowerState></PowerState>
        <ActiveCoolingLevel></ActiveCoolingLevel>
        <ActiveCoolingDeviceIndex></ActiveCoolingDeviceIndex>
    </ActiveCoolingDevicePower>
  </ThermalEvents>
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
<td align="left"><strong>&lt;悪意のあるイベント&gt;</strong></td>
<td align="left"><p>すべての異なる温度イベントが含まれます。 PwrTest ログファイル内に存在できるのは、1つのテストの<strong> &lt; イベント &gt; </strong>要素だけです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EnteringCS&gt;</strong></td>
<td align="left"><p>コネクトスタンバイ (CS) エントリが開始されました。システムは、ディスプレイがオフになり、入力が無効になるとすぐに CS にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExitingCS&gt;</strong></td>
<td align="left"><p>CS の終了を開始しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExitedCS&gt;</strong></td>
<td align="left"><p>CS の終了が完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AbortingCS&gt;</strong></td>
<td align="left"><p>最も深いフェーズに入る前に CS エントリが中止され、終了します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AbortedCS&gt;</strong></td>
<td align="left"><p>中止されたエントリの後に CS 終了が完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InputDisabled&gt;</strong></td>
<td align="left"><p>ユーザー入力がローカルコンソールで無効になっています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;InputEnabled&gt;</strong></td>
<td align="left"><p>ローカルコンソールでユーザー入力が有効になりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PhaseEnter&gt;</strong></td>
<td align="left"><p>CS フェーズが入力されました。 name 属性は CS フェーズの名前です。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PhaseExit&gt;</strong></td>
<td align="left"><p>CS フェーズが終了しました。 name 属性は CS フェーズの名前です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredSet&gt;</strong></td>
<td align="left"><p>プロセスが実行が必要な要求を実行しました。これにより、DAM フェーズの完了がブロックされます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredCleared クリアされました&gt;</strong></td>
<td align="left"><p>プロセスが、DAM フェーズの完了をブロックする実行が必要な要求を消去しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PlatformIdleStats&gt;</strong></td>
<td align="left"><p>Platform idle statistics block。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;状態&gt;</strong></td>
<td align="left"><p>以前のプラットフォームアイドル統計ブロック以降のプラットフォームアイドル状態の移行回数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest の構文](pwrtest-syntax.md)

[PowerCfg](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options)

 

 






