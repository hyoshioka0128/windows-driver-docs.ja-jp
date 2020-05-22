---
title: PwrTest の要求シナリオ
description: PwrTest Requests シナリオでは、システムで実行されているプロセスとサービスからの電力要求が発生したときにログに記録されます。
ms.assetid: 4B082680-5C43-45F6-9A0E-0C23E9B1F282
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2685134af91507fdf9b08bd69977825db0c9691a
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769658"
---
# <a name="pwrtest-requests-scenario"></a>PwrTest の要求シナリオ


PwrTest Requests シナリオでは、システムで実行されているプロセスとサービスからの電力要求が発生したときにログに記録されます。

PwrTest 要求シナリオを使用すると、コンピューターがスリープ状態にならない原因、またはモニターが常時稼働している理由を診断できます。

また、管理者ツール[powercfg](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options) (powercfg) をこの目的に使用することもできます (powercfg **/要求**)。 PowerCfg は Windows (Windows System32 ディレクトリ) に含まれてい \\ ます。 ただし、Powercfg は、ツールの実行時にアクティブな電源要求のみをキャプチャします。 これに対して、PwrTest Requests シナリオは、指定された時間に実行され、作成および終了時には電力要求をログに記録するため、ツールの実行時に要求をアクティブにする必要はありません。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


```
pwrtest /requests [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**/t:**<em>n</em>  
シナリオが実行されるまでの合計時間 (分) を指定します ( *n*の既定値は30分です)。

**例**

```
pwrtest /requests  
```

```
pwrtest /requests  /t:60
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PowerRequests> 
    <CreatePowerRequestEvent>
        <Timestamp></TimeStamp>
        <Caller></Caller>
        <Context></Context>
        <RequestObject></RequestObject>
        <Type></Type>
        <ProcessID></ProcessID>
        <SessionID></SessionID>
        <Legacy></Legacy>
        <SystemAllowed></SystemAllowed>
        <DisplayAllowed></DisplayAllowed>
        <AwayModeAllowed></AwayModeAllowed>
        <PerfBoostAllowed></PerfBoostAllowed>
        <ExecutionRequiredAllowed></ExecutionRequiredAllowed>    
        <SystemCount></SystemCount>
        <DisplayCount></DisplayCount>
        <AwayModeCount></AwayModeCount>
        <PerfBoostCount></PerfBoostCount>
        <ExecutionRequiredCount></ExecutionRequiredCount>
    </CreatePowerRequestEvent>
    <ChangePowerRequestEvent>
        <Timestamp></TimeStamp>
        <Caller></Caller>
        <RequestObject></RequestObject>
        <SystemCount></SystemCount>
        <DisplayCount></DisplayCount>
        <AwayModeCount></AwayModeCount>
        <PerfBoostCount></PerfBoostCount>
        <ExecutionRequiredCount></ExecutionRequiredCount>
    </ChangePowerRequestEvent>
    <ClosePowerRequestEvent>
        <Timestamp></TimeStamp>
        <Caller></Caller>
        <RequestObject></RequestObject>
    </ClosePowerRequestEvent>
  </PowerRequests>
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
<td align="left"><strong>&lt;PowerRequests&gt;</strong></td>
<td align="left"><p>すべての異なる電源要求イベントを格納します。 PwrTest ログファイルには、 <strong> &lt; powerrequests &gt; </strong>要素を1つだけ指定できます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;Caller&gt;</strong></td>
<td align="left"><p>要求元の名前。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;コンテキスト&gt;</strong></td>
<td align="left"><p>デバイスインスタンスパス (該当する場合)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RequestObject&gt;</strong></td>
<td align="left"><p>イベントの要求オブジェクト。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Type&gt;</strong></td>
<td align="left"><p>呼び出し元の数値型。</p>
<p>0 = ドライバー</p>
<p>1 = プロセス</p>
<p>2 = 共有サービス</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ProcessID&gt;</strong></td>
<td align="left"><p>呼び出し元のプロセス ID。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SessionID&gt;</strong></td>
<td align="left"><p>プロセスの場合は、呼び出し元のセッション ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;従来&gt;</strong></td>
<td align="left"><p>呼び出し元が従来の<a href="https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setthreadexecutionstate" data-raw-source="[&lt;strong&gt;SetThreadExecutionState function (Windows)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setthreadexecutionstate)"><strong>SetThreadExecutionState 関数 (windows)</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate" data-raw-source="[&lt;strong&gt;PoSetSystemState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-posetsystemstate)"><strong>Posetsystemstate</strong></a> Api または新しい<a href="https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-powersetrequest" data-raw-source="[&lt;strong&gt;PowerSetRequest function (Windows)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-powersetrequest)"><strong>powersetrequest 関数 (Windows)</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerrequest" data-raw-source="[&lt;strong&gt;PoSetPowerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerrequest)"><strong>posetsystemstate</strong></a> api を使用している場合は、True または False を報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SystemAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元に対してシステム要求が許可されているかどうかを報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元に対して表示要求が許可されているかどうかを報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayModeAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元に対して、退席モード要求が許可されているかどうかを報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerfBoostAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元に対してパフォーマンス向上要求が許可されているかどうかを報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元に対して必要な実行要求が許可されているかどうかを報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SystemCount&gt;</strong></td>
<td align="left"><p>この呼び出し元に対するシステム要求の数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DisplayCount&gt;</strong></td>
<td align="left"><p>この呼び出し元に対する表示要求の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AwayModeCount&gt;</strong></td>
<td align="left"><p>この呼び出し元に対する退席モード要求の数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerfBoostCount&gt;</strong></td>
<td align="left"><p>この呼び出し元に対するパフォーマンス向上要求の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredCount&gt;</strong></td>
<td align="left"><p>この呼び出し元に対して実行する必要のある要求の数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CreatePowerRequestEvent&gt;</strong></td>
<td align="left"><p>呼び出し元が新しい要求を作成しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ChangePowerRequestEvent&gt;</strong></td>
<td align="left"><p>呼び出し元が要求数を変更しました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ClosePowerRequestEvent&gt;</strong></td>
<td align="left"><p>呼び出し元が要求を終了しました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest の構文](pwrtest-syntax.md)

[PowerCfg](https://docs.microsoft.com/windows-hardware/design/device-experiences/powercfg-command-line-options)

 

 






