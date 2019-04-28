---
title: PwrTest の温度シナリオ
description: PwrTest 熱のシナリオでは、ACPI 熱のゾーンの情報と統計情報を監視します。
ms.assetid: C6941A50-EA0F-4C46-A290-8CAAD292E156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92add792882c0a50b7697b1976181fbf2e2a10c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380958"
---
# <a name="pwrtest-thermal-scenario"></a>PwrTest の温度シナリオ


PwrTest 熱のシナリオでは、ACPI 熱のゾーンの情報と統計情報を監視します。 このシナリオは、温度のゾーンと気温の変化を報告するシステムでのみサポートされます。

**注**このシナリオは、オペレーティング システムに温度データを報告するシステムでのみ機能します。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /thermal [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

<span id="_temp_kcf"></span><span id="_TEMP_KCF"></span>**/temp:**{**k**|**c**|**f**}  
ケルビンの温度尺度を指定します (**k**)、摂氏 (**c**)、華氏 (**f**) すべての出力とログ記録を使用する (既定値はケルビン)。

**使用例**

```
pwrtest /thermal  
```

```
pwrtest /thermal  /t:30
```

```
pwrtest /thermal  /t:30 /temp:f
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

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
<td align="left"><strong>&lt;ThermalEvents&gt;</strong></td>
<td align="left"><p>すべての別の温度のイベントが含まれています。 1 つのみ<strong>&lt;ThermalEvents&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EnteringCS&gt;</strong></td>
<td align="left"><p>接続されたスタンバイ (CS) の開始、システムにエントリが CS とすぐに表示をオフになった入力が無効になっています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExitingCS&gt;</strong></td>
<td align="left"><p>CS 終了を開始します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExitedCS&gt;</strong></td>
<td align="left"><p>CS 終了が完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AbortingCS&gt;</strong></td>
<td align="left"><p>CS エントリを中止し、最下位のフェーズに入る前に終了します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AbortedCS&gt;</strong></td>
<td align="left"><p>CS 終了が中止されたエントリの後に完了しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InputDisabled&gt;</strong></td>
<td align="left"><p>ローカルのコンソールで、ユーザー入力が無効にされました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;InputEnabled&gt;</strong></td>
<td align="left"><p>ユーザー入力は、ローカルのコンソールで有効にされました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PhaseEnter&gt;</strong></td>
<td align="left"><p>CS フェーズは、入力された名前の属性が CS フェーズの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PhaseExit&gt;</strong></td>
<td align="left"><p>CS フェーズが終了した、名前の属性が CS フェーズの名前。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredSet&gt;</strong></td>
<td align="left"><p>プロセスには、ダム フェーズの完了をブロックする実行の必要な要求が行われます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredCleared&gt;</strong></td>
<td align="left"><p>プロセスでは、ダム フェーズの完了にブロックを解除する実行の必要な要求をクリアします。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PlatformIdleStats&gt;</strong></td>
<td align="left"><p>アイドル状態の統計情報ブロックのプラットフォームです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;状態&gt;</strong></td>
<td align="left"><p>以前のプラットフォームのアイドル状態の統計情報ブロックのためのプラットフォームのアイドル状態の遷移の数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

[PowerCfg](https://go.microsoft.com/fwlink/p/?linkid=294568)

 

 






