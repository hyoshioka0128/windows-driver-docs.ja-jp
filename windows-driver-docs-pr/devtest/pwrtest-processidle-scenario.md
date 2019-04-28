---
title: PwrTest のプロセス アイドル シナリオ
description: PwrTest ProcessIdle シナリオでは、(ここではなく、スケジュールされた時刻) を実行するバック グラウンドのメンテナンス タスクおよびその進行状況を監視します。
ms.assetid: 14932191-C956-4623-AF62-5A6650D72164
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8768034c5c4dc1b1cd189d9489a141c1883979f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382664"
---
# <a name="pwrtest-processidle-scenario"></a>PwrTest のプロセス アイドル シナリオ


PwrTest ProcessIdle シナリオでは、(ここではなく、スケジュールされた時刻) を実行するバック グラウンドのメンテナンス タスクおよびその進行状況を監視します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /processidle [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
その後、待機が中止された、実行するには、シナリオの場合でも、アイドル状態のタスクが実行を継続しています最大時間 (分) を指定します (既定では、すべてのタスクを完了するまで実行)。

**使用例**

```
pwrtest /processidle  
```

```
pwrtest /processidle  /t:30
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <ProcessIdle> 
    <JobStart>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobStart>
    <JobEndSuccess>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobEndSuccess>
    <JobEndFailure>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobEndFailure>
    <JobEndTermination>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobEndTermination>
    <JobCompletionPending>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
    </JobCompletionPending>
    <IdleTaskRegister>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskRegister>
    <IdleTaskUnregister>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskUnregister>
    <IdleTaskStart>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskStart>
    <IdleTaskStop>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskStop>
    <IdleTaskNotifyStart>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskNotifyStart>
    <IdleTaskNotifyComplete>
      <Timestamp></Timestamp>
      <TaskName></TaskName>
      <ProcessId></ProcessId>
    </IdleTaskNotifyComplete>
    <OtherProcessIdleTasksCallsInProgress>
      <Timestamp></Timestamp>
    </OtherProcessIdleTasksCallsInProgress>
  </ProcessIdle>
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
<td align="left"><strong>&lt;ProcessIdle&gt;</strong></td>
<td align="left"><p>すべての別のプロセス アイドル イベントが含まれています。 1 つだけ<strong>&lt;ProcessIdle&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TaskName&gt;</strong></td>
<td align="left"><p>アイドル状態のタスクの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;プロセス Id&gt;</strong></td>
<td align="left"><p>アイドル状態のタスクのプロセス ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobStart&gt;</strong></td>
<td align="left"><p>イベントは、ジョブの開始を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;JobEndSuccess&gt;</strong></td>
<td align="left"><p>イベントは、ジョブが正常に終了を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobEndFailure&gt;</strong></td>
<td align="left"><p>イベントでは、ジョブが失敗したことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;JobEndTermination&gt;</strong></td>
<td align="left"><p>イベントは、ジョブが早期終了を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;JobCompletionPending&gt;</strong></td>
<td align="left"><p>イベントを示しますジョブの完了が保留中です。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskRegister&gt;</strong></td>
<td align="left"><p>イベントは、アイドル状態のタスクの登録を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskUnregister&gt;</strong></td>
<td align="left"><p>イベントは、アイドル状態のタスクは、登録されたことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskStart&gt;</strong></td>
<td align="left"><p>イベントは、アイドル状態のタスクの開始を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskStop&gt;</strong></td>
<td align="left"><p>アイドル状態のタスクが停止したことを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleTaskNotifyStart&gt;</strong></td>
<td align="left"><p>イベントは、プロセスがアイドル状態のタスクを呼び出すを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleTaskNotifyComplete&gt;</strong></td>
<td align="left"><p>イベントがプロセスを示しますがアイドル状態のタスクの呼び出しを完了します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;OtherProcessIdleTasksCallsInProgress&gt;</strong></td>
<td align="left"><p>イベントと呼ばれる別のプロセスを示す、 <strong>ProcessIdleTasks</strong>バック グラウンドでの関数。 Pwrtest を呼び出す、 <strong>ProcessIdleTasks</strong> advapi32.dll によってエクスポートされる関数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






