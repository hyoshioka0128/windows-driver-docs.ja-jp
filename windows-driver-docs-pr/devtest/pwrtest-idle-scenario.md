---
title: PwrTest のアイドル シナリオ
description: PwrTest アイドル状態のシナリオは、ユーザーを監視し、CPU アイドル状態の統計情報は 15 秒ごとにカーネルによって収集されたアイドル状態の統計情報を表示します。
ms.assetid: 7E40DD91-D236-41B3-BC3A-DEB6DDD76139
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2d7606d97a1bb410b7920b26e1b485193e08985
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569645"
---
# <a name="pwrtest-idle-scenario"></a>PwrTest のアイドル シナリオ


PwrTest アイドル状態のシナリオは、ユーザーを監視し、CPU アイドル状態の統計情報は 15 秒ごとにカーネルによって収集されたアイドル状態の統計情報を表示します。

このシナリオと組み合わせることができます、 [PwrTest 実行状態シナリオ](pwrtest-execution-state-scenario.md)(**/es**) レガシの実行を同時に監視する状態の変更することができますを診断するシステムがアイドル状態をしない理由スリープ状態にします。

**注**  これは、従来のシナリオと推奨される置き換えは、 [PwrTest PPM シナリオ](pwrtest-ppm-scenario.md)(**/ppm**) CPU アイドル状態の統計を監視するため、 [PwrTest モニター シナリオ](pwrtest-monitor-scenario.md)(**監視/**) のユーザーがアイドル状態を監視します。

 

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /idle  [/t:n] [/?] [/es [es_options]
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

<span id="_es___es_options_"></span><span id="_ES___ES_OPTIONS_"></span>**/es \[**<em>es\_options</em>**\]**  
実行、 [PwrTest 実行状態 (ES) のシナリオ](pwrtest-execution-state-scenario.md)します。

**例**

```
pwrtest /idle /t:60
```

```
pwrtest /idle /es /user
```

```
pwrtest /idle /es /kernel
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PowerIdleStatistics> 
    <IdleStats> 
      <Time></Time>
      <Threshold></Threshold>
      <LowestIdleness></LowestIdleness>
      <AverageIdleness></AverageIdleness>
      <AccruedIdleTime></AccruedIdleTime>
      <NonIdleIgnored></NonIdleIgnored>
      <IdleToSleep></IdleToSleep>
      <NonIdleReferences></NonIdleReferences>
    </IdleStats>
    <EsChange> 
      <Time>XX:XX:XX</Time>
      <Process></Process>
        <RawState></RawState>
        <Continuous></Continuous>
        <System></System>
        <Display></Display>
        <AwayMode></AwayMode>
    </EsChange> 
  </PowerIdleStatistics>
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
<td align="left"><strong>&lt;PowerIdleStatistics&gt;</strong></td>
<td align="left"><p>アイドル状態のシナリオのシナリオに関連する情報が含まれています。 1 つだけ<strong>&lt;PowerIdleStatistics&gt;</strong> PwrTest ログ ファイルに要素を表示できます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleStats&gt;</strong></td>
<td align="left"><p>最後のアイドル時間のアイドル状態の統計情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;時間&gt;</strong></td>
<td align="left"><p>最新のアイドル状態の統計イベントの時刻。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;しきい値&gt;</strong></td>
<td align="left"><p>アイドル状態のしきい値を無視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;LowestIdleness&gt;</strong></td>
<td align="left"><p>期間の最も低いアイドル割合。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AverageIdleness&gt;</strong></td>
<td align="left"><p>期間の平均アイドル割合。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTime&gt;</strong></td>
<td align="left"><p>未収期間中のアイドル時間。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;NonIdleIgnored&gt;</strong></td>
<td align="left"><p>期間中に無視されましたが非アイドル時間。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleToSleep&gt;</strong></td>
<td align="left"><p>期間中にスリープ状態には、システムはアイドル状態でしたでしょうか。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;NonIdleReferences&gt;</strong></td>
<td align="left"><p>非アイドルの量は、期間中に参照を無視します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EsChange&gt;</strong></td>
<td align="left"><p>含む 1 つのスレッドの実行状態変更イベントに関連する情報。 される<strong>&lt;EsChange&gt;</strong> PwrTest ログ ファイルに記録された各スレッドの実行状態変更イベントの要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;時間&gt;</strong></td>
<td align="left"><p>実行状態変更イベントが発生した時刻を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;プロセス&gt;</strong></td>
<td align="left"><p>実行状態の変更を要求するプロセスのイメージ ファイルへのパスを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;RawState&gt;</strong></td>
<td align="left"><p>要求の実行状態を示します。 これは EXECUTION_STATE 型の 32 ビット値です (Windows.h を参照してください)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;継続的です&gt;</strong></td>
<td align="left"><p>プロセスに継続的な (ES_CONTINUOUS) かどうかを実行状態の変更が要求された場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;システム&gt;</strong></td>
<td align="left"><p>プロセスが使用可能な (ES_SYSTEM_REQUIRED) にするか、システムを要求された場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;表示&gt;</strong></td>
<td align="left"><p>プロセスが使用可能な (ES_DISPLAY_REQUIRED) かどうかを表示を要求された場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayMode&gt;</strong></td>
<td align="left"><p>あるプロセスの要求された退席中モードかどうか (ES_AWAYMODE_REQUIRED) が有効にした場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






