---
title: PwrTest タイマーのシナリオ
description: PwrTest タイマーのシナリオが発生したときに、システムのタイマー精度変更を記録します。
ms.assetid: 842A827F-8046-4A31-938B-B1EA2119421A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a051682ae6582f6d3a91bffdafd85772848dc196
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532875"
---
# <a name="pwrtest-timer-scenario"></a>PwrTest タイマーのシナリオ


PwrTest タイマーのシナリオが発生したときに、システムのタイマー精度変更を記録します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /timer /?  [/t:n]  [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

**例**

```
  pwrtest /timer
```

```
pwrtest /timer /t:5
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <TimerEvents> 
    <TimerResolutionRundown>
      <Timestamp></Timestamp>
      <CurrentResolution></CurrentResolution>
      <MinimumResolution></MinimumResolution>
      <MaximumResolution></MaximumResolution>
      <KernelCount></KernelCount>
      <KernelResolution></KernelResolution>
    </TimerResolutionRundown>
    <TimerResolutionRequestRundown>
        <Timestamp></Timestamp>
        <AppName></AppName>
        <Resolution></Resolution>
        <ProcessID></ProcessID>
    </TimerResolutionRequestRundown>
    <NtSetTimerResolution>
      <Timestamp></Timestamp>
      <AppName></AppName>
      <ServiceName></ServiceName>
      <Resolution></Resolution>
      <ProcessID></ProcessID>
    </NtSetTimerResolution>
    <UpdateTimerResolution>
      <Timestamp></Timestamp>
      <Resolution></Resolution>
    </UpdateTimerResolution>
    <ExSetTimerResolution>
      <Timestamp></Timestamp>
      <Resolution></Resolution>
    </ExSetTimerResolution>  
  </TimerEvents>
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
<td align="left"><strong>&lt;TimerEvents&gt;</strong></td>
<td align="left"><p>すべての個々 のタイマー イベントが含まれています。 1 つだけ<strong>&lt;TimerEvents&gt;</strong> PwrTest ログ ファイルに要素を表示できます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimerResolutionRundown&gt;</strong></td>
<td align="left"><p>現在表示するイベント タイマーの解決の統計情報。 これらのイベントの 1 つだけが記録されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CurrentResolution&gt;</strong></td>
<td align="left"><p>現在の解像度 (ミリ秒単位)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;MinimumResolution&gt;</strong></td>
<td align="left"><p>最小解像度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MaximumResolution&gt;</strong></td>
<td align="left"><p>最大解像度。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;KernelCount&gt;</strong></td>
<td align="left"><p>カーネル モードから解決要求の数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;KernelResolution&gt;</strong></td>
<td align="left"><p>現在のカーネルのタイマー精度。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimerResolutionRequestRundown&gt;</strong></td>
<td align="left"><p>イベントが現在解決要求を表示します。 複数のイベントを記録する可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AppName&gt;</strong></td>
<td align="left"><p>要求元のプロセスの名前です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;解決方法&gt;</strong></td>
<td align="left"><p>ミリ秒単位の要求の解像度。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;プロセス Id&gt;</strong></td>
<td align="left"><p>要求元のプロセス ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NtSetTimerResolution&gt;</strong></td>
<td align="left"><p>イベントが行われるプロセスを示しますタイマーの解決の要求。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;サービス名&gt;</strong></td>
<td align="left"><p>該当する場合、要求元のサービスの名前。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;UpdateTimerResolution&gt;</strong></td>
<td align="left"><p>イベントでは、タイマー精度が更新されたことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExSetTimerResolution&gt;</strong></td>
<td align="left"><p>イベントは、カーネル コンポーネントを示します。 タイマーの解決の要求。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






