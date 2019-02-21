---
title: PwrTest バッテリ シナリオ
description: PwrTest バッテリのシナリオは、バッテリと電源のソース情報の自動の検査を容易に設計されています。
ms.assetid: e0bad871-a826-4951-9a84-93c9b1aa0653
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37c7323d6b3ff4a5cb1b299ebc0acade9cd1707f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531326"
---
# <a name="pwrtest-battery-scenario"></a>PwrTest バッテリ シナリオ


PwrTest バッテリのシナリオは、バッテリと電源のソース情報の自動の検査を容易に設計されています。

PwrTest はバッテリ容量、電圧、ドレイン、および多くのバッテリがシステム内の一般的な状態の割合をログ記録できます。 バッテリのデータは、サイクルの指定した数の指定された間隔で記録されます。

### <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文

```
pwrtest /battery [/c:n] [/i:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c:**<em>n</em>  
実行するには、(既定値は 100) サイクルの数を指定します。

<span id="_i_n"></span><span id="_I_N"></span>**/i:**<em>n</em>  
(既定値は 5000) をミリ秒単位でのポーリング間隔を指定します。

**例**

```
pwrtest /battery 
```

```
pwrtest /battery /c:4 /i:1000
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <BatteryScenario>
    <Batteries>
      <Battery id="" shortterm="" rechargable="" >
        <Name></Name>
        <UniqueID></UniqueID>
        <Chemistry></Chemistry>
        <Manufacturer></Manufacturer>
        <DesignedCapacity></DesignedCapacity>
        <FullChargeCapacity></FullChargeCapacity>
        <CriticalBias></CriticalBias>
        <CycleCount></CycleCount>
        <ManufactureDate></ManufactureDate>
        <FullLifeTime Units=""></FullLifeTime>
      </Battery> 
    </Batteries>
    <BatteryTraces interval="">
      <Trace>
        <ElapsedT></ElapsedT>
        <ACStatus></ACStatus>
        <Capacity id=""></Capacity>
        <TimeRemaining></TimeRemaining>
        <Capacity id=""></Capacity>
        <RateOfDrain id=””></RateOfDrain>
        <Voltage id=””></Voltage>
        <Capacity id=""></Capacity>
        <RateOfDrain id=””></RateOfDrain>
        <Voltage id=””> </Voltage>
      </Trace>
    </BatteryTraces> 
  </BatteryScenario>
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
<td align="left"><strong>&lt;一意の Id&gt;</strong></td>
<td align="left"><p>バッテリの一意の ID を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;化学&gt;</strong></td>
<td align="left"><p>バッテリ化学を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;製造元&gt;</strong></td>
<td align="left"><p>バッテリの製造元を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DesignedCapacity&gt;</strong></td>
<td align="left"><p>ミリワット時間 (mw-h 消費) で、バッテリの設計容量を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FullChargeCapacity&gt;</strong></td>
<td align="left"><p>ミリワット時間 (mw-h 消費) で完全に充電されたバッテリの容量を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CriticalBias&gt;</strong></td>
<td align="left"><p>バッテリのレポートに適用される mW h での 0 から、バイアスを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CycleCount&gt;</strong></td>
<td align="left"><p>バッテリが発生した料金/放電サイクル数を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ManufactureDate&gt;</strong></td>
<td align="left"><p>バッテリの製造日を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;FullLifeTime&gt;</strong></td>
<td align="left"><p>秒でバッテリの完全な有効期間を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;BatteryTraces&gt;</strong></td>
<td align="left"><p>一覧を含む<strong>&lt;トレース&gt;</strong>要素。 バッテリ情報のポーリング間隔を示す属性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;トレース&gt;</strong></td>
<td align="left"><p>指定した間隔の電圧、容量の消費率などのバッテリの状態に関する情報が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ElapsedT&gt;</strong></td>
<td align="left"><p>PwrTest が開始されてから経過した時間を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ACStatus&gt;</strong></td>
<td align="left"><p>(1) AC またはバッテリ (0) で、システムが実行されているかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;TimeRemaining&gt;</strong></td>
<td align="left"><p>秒単位で残りのすべてのシステム バッテリからバッテリ寿命の時間を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;容量&gt;</strong></td>
<td align="left"><p>ミリワット時間 (mw-h 消費) で、バッテリの容量を示します。 容量が報告されているどのバッテリを示すために id 属性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RateOfDrain&gt;</strong></td>
<td align="left"><p>ミリ ワット (mW) で、バッテリの消耗の速度を示します。 ドレインのレートが報告されているどのバッテリを示すために ID 属性があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;電圧&gt;</strong></td>
<td align="left"><p>ミリボルト (mV) でバッテリ電圧を示します。 電圧が報告されているどのバッテリを示すために ID 属性があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






