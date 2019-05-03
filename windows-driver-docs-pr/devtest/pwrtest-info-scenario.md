---
title: PwrTest の情報シナリオ
description: PwrTest 情報シナリオは、キャプチャし、さまざまなカテゴリから現在のシステム電源の情報を記録します。
ms.assetid: 1d13d1dd-eb8d-434a-b994-e747a86f3457
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ad34aa2d7ebb5e520be61fea1505fbe7a2fddfe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382696"
---
# <a name="pwrtest-info-scenario"></a>PwrTest の情報シナリオ


PwrTest 情報シナリオは、キャプチャし、さまざまなカテゴリから現在のシステム電源の情報を記録します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /info:option [/p:{n|a|*}] [/w:n]  [/?] 
```

<span id="_info_option"></span><span id="_INFO_OPTION"></span>**/info:**<em>option</em>  

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>オプション</em></th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="all"></span><span id="ALL"></span><strong>すべての</strong></p></td>
<td align="left"><p>すべてのシステム情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="powercap"></span><span id="POWERCAP"></span><strong>powercap</strong></p></td>
<td align="left"><p>SYSTEM_POWER_CAPABILITIES を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="powerinfo"></span><span id="POWERINFO"></span><strong>powerinfo</strong></p></td>
<td align="left"><p>SYSTEM_POWER_CAPABILITIES を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="battery"></span><span id="BATTERY"></span><strong>バッテリ</strong></p></td>
<td align="left"><p>SYSTEM_BATTERY_STATE を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ppm"></span><span id="PPM"></span><strong>ppm</strong></p></td>
<td align="left"><p>すべてのプロセッサ情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ppmidle"></span><span id="PPMIDLE"></span><strong>ppmidle</strong></p></td>
<td align="left"><p>プロセッサのアイドル状態の情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="ppmperf"></span><span id="PPMPERF"></span><strong>ppmperf</strong></p></td>
<td align="left"><p>プロセッサ パフォーマンスの状態情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="ppmperfverbose"></span><span id="PPMPERFVERBOSE"></span><strong>ppmperfverbose</strong></p></td>
<td align="left"><p>詳細形式では、プロセッサのパフォーマンスの状態情報を表示します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_p_na_"></span><span id="_P_NA_"></span>**/p:**{*n*|**a**|**\\***}  

論理プロセッサ数を指定します **/info:ppm/info: ppmidle**、または **/info:ppmperf**オプション。

<span id="a_or__"></span><span id="A_OR__"></span>または \\*********  
すべての論理プロセッサ (既定値) を指定します。

<span id="_w_yn"></span><span id="_W_YN"></span>**/w:**{**y**|**n**}  
PPM ランダウン イベントを待機する秒単位で時間を指定します (既定値は 10 秒)。

**使用例**

```
pwrtest /info:all
```

```
  pwrtest /info:battery
```

```
  pwrtest /info:ppm
```

```
  pwrtest /info:ppm /p:1
```

```
 pwrtest /info:ppmidle
```

```
  pwrtest /info:ppmperf /p:2
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <InfoScenario>
    <SYSTEM_POWER_CAPABILITIES> 
      <SystemS1StateSupported></SystemS1StateSupported>
      <SystemS2StateSupported></SystemS2StateSupported>
      <SystemS3StateSupported></SystemS3StateSupported>
      <SystemS4StateSupported></SystemS4StateSupported>
      <SystemS5StateSupported></SystemS5StateSupported>
      <RtcWakeSupported></RtcWakeSupported>
      <FastSystemS4></FastSystemS4>
    </SYSTEM_POWER_CAPABILITIES> 
    <SYSTEM_POWER_INFORMATION> 
      <MaxIdlenessAllowed></MaxIdlenessAllowed>
      <Idleness></Idleness>
      <TimeRemaining></TimeRemaining>
      <CoolingMode></CoolingMode>
    </SYSTEM_POWER_INFORMATION> 
    <SYSTEM_BATTERY_STATE> 
      <AcOnLine></AcOnLine>
      <BatteryPresent></BatteryPresent>
      <Charging></Charging>
      <Discharging></Discharging>
      <MaxCapacity></MaxCapacity>
      <RemainingCapacity></RemainingCapacity>
      <RateOfDrain></RateOfDrain>
      <EstimatedTime></EstimatedTime>
      <DefaultAlert1></DefaultAlert1>
      <DefaultAlert2></DefaultAlert2>
    </SYSTEM_BATTERY_STATE> 
    <PROCESSOR_POWER_INFORMATION> 
      <CPUNumber></CPUNumber>
      <MaxMhz></MaxMhz>
      <CurrentMhz></CurrentMhz>
      <MhzLimit></MhzLimit>
      <MaxIdleState></MaxIdleState>
      <CurrentIdleState></CurrentIdleState>
    </PROCESSOR_POWER_INFORMATION> 
    </InfoScenario>
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
<td align="left"><strong>&lt;InfoScenario&gt;</strong></td>
<td align="left"><p>情報のシナリオに関連する情報が含まれています。 1 つしかない<strong>&lt;InfoScenario&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SYSTEM_POWER_CAPABILITIES&gt;</strong></td>
<td align="left"><p>システム電源の機能に関連する情報が含まれています。 この情報は、SYSTEM_POWER_CAPABILITIES 構造体から取得されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SystemSxStateSupported&gt;</strong></td>
<td align="left"><p>システム ACPI のスリープ状態がシステムでサポートされているかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RtcWakeSupported&gt;</strong></td>
<td align="left"><p>RTC ウェイク アップ (タイマーにスリープ解除) がサポートされている最下位のスリープ状態を示します。 値は、SYSTEM_POWER_STATE 列挙体のです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FastSystemS4&gt;</strong></td>
<td align="left"><p>ハイブリッド スリープは、システムで使用できるかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SYSTEM_POWER_INFORMATION&gt;</strong></td>
<td align="left"><p>システムのアイドルに関連する情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MaxIdlenessAllowed&gt;</strong></td>
<td align="left"><p>(パーセント) でアイドルを示す、システムがアイドル状態と見なされます、アイドルのタイムアウトは、カウントを開始します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;アイドル&gt;</strong></td>
<td align="left"><p>割合で表される、現在アイドル状態のレベル。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimeRemaining&gt;</strong></td>
<td align="left"><p>秒単位で、システムのスタンバイ アイドル タイマーの残りの期間を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CoolingMode&gt;</strong></td>
<td align="left"><p>現在のモードを冷却システムを示します。アクティブ (0)、(1)、"Passive"、(2) が無効です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SYSTEM_BATTERY_STATE&gt;</strong></td>
<td align="left"><p>システム バッテリの現在の状態に関連する情報が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AcOnLine&gt;</strong></td>
<td align="left"><p>システムが AC 電源で現在動作するかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BatteryPresent&gt;</strong></td>
<td align="left"><p>少なくとも 1 つのバッテリがシステムに存在するかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;充電中&gt;</strong></td>
<td align="left"><p>少なくとも 1 つのバッテリが現在充電中かどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;放電しています&gt;</strong></td>
<td align="left"><p>少なくとも 1 つのバッテリは放電して現在あるかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaxCapacity&gt;</strong></td>
<td align="left"><p>新しいミリワット時間 (mw-h 消費) で、ときに、バッテリの最大容量。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RemainingCapacity&gt;</strong></td>
<td align="left"><p>ミリワット時間 (mw-h 消費) では、バッテリの残りの容量を推定します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RateOfDrain&gt;</strong></td>
<td align="left"><p>ミリ ワット (mW) で、バッテリの放電の現在の速度を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EstimatedTime&gt;</strong></td>
<td align="left"><p>秒単位で、バッテリの残り時間。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DefaultAlert1&gt;</strong></td>
<td align="left"><p>バッテリのアラートが発生するときは、バッテリの製造元の推奨される容量を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DefaultAlert2&gt;</strong></td>
<td align="left"><p>バッテリ警告が発生するときは、バッテリの製造元の推奨される容量を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PROCESSOR_POWER_INFORMATION&gt;</strong></td>
<td align="left"><p>システムのプロセッサと、電源管理機能に関連する情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CPUNumber&gt;</strong></td>
<td align="left"><p>現在のプロセッサを示す&lt;PROCESSOR_POWER_INFORMATION&gt;要素を記述します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaxMhz&gt;</strong></td>
<td align="left"><p>プロセッサの最大の頻度を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CurrentMhz&gt;</strong></td>
<td align="left"><p>プロセッサの現在の頻度を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MhzLimit&gt;</strong></td>
<td align="left"><p>プロセッサのクロック周波数に対する現在の制限を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MaxIdleState&gt;</strong></td>
<td align="left"><p>プロセッサの最大のアイドル状態を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CurrentIdleState&gt;</strong></td>
<td align="left"><p>プロセッサの現在のアイドル状態を示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






