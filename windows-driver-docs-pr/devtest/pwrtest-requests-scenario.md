---
title: PwrTest の要求シナリオ
description: PwrTest 要求のシナリオでは、プロセスとが発生したときに、システムで実行されているサービスから power 要求を記録します。
ms.assetid: 4B082680-5C43-45F6-9A0E-0C23E9B1F282
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c37c836e0643ef6099b72aa532fbc19e66ca8fd4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356404"
---
# <a name="pwrtest-requests-scenario"></a>PwrTest の要求シナリオ


PwrTest 要求のシナリオでは、プロセスとが発生したときに、システムで実行されているサービスから power 要求を記録します。

PwrTest 要求のシナリオを使用すると、コンピューターがスリープまたはモニター上に留まります理由に移動しない原因を診断します。

管理者ツールを使用することも[PowerCfg](https://go.microsoft.com/fwlink/p/?linkid=294568) (powercfg.exe) この目的のため (**powercfg.exe/requests**)。 PowerCfg を Windows に含まれている (Windows\\System32 ディレクトリ)。 ただし、Powercfg.exe はツールの実行時にアクティブになっている電源要求のみをキャプチャします。 これに対し、PwrTest 要求シナリオが、指定した時間実行され、ログ電力要求が作成され、閉じられたため、要求は、ツールの実行時にアクティブ化する必要はありません。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /requests [/t:n] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:** <em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

**使用例**

```
pwrtest /requests  
```

```
pwrtest /requests  /t:60
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

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
<td align="left"><strong>&lt;PowerRequests&gt;</strong></td>
<td align="left"><p>別の電源のすべての要求イベントが含まれています。 1 つのみ<strong>&lt;PowerRequests&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;呼び出し元&gt;</strong></td>
<td align="left"><p>要求元の名前です。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;コンテキスト&gt;</strong></td>
<td align="left"><p>デバイス インスタンスのパスを該当する場合</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RequestObject&gt;</strong></td>
<td align="left"><p>イベントのオブジェクトを要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;型&gt;</strong></td>
<td align="left"><p>呼び出し元の数値型。</p>
<p>0 = ドライバー</p>
<p>1 = プロセス</p>
<p>2 = 共有サービス</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;プロセス Id&gt;</strong></td>
<td align="left"><p>呼び出し元のプロセス ID。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SessionID&gt;</strong></td>
<td align="left"><p>プロセスの場合、呼び出し元のセッション ID。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;レガシ&gt;</strong></td>
<td align="left"><p>呼び出し元は、レガシを使用する場合、True または False を報告<a href="https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setthreadexecutionstate" data-raw-source="[&lt;strong&gt;SetThreadExecutionState function (Windows)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-setthreadexecutionstate)"> <strong>SetThreadExecutionState 関数 (Windows)</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-posetsystemstate" data-raw-source="[&lt;strong&gt;PoSetSystemState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-posetsystemstate)"> <strong>PoSetSystemState</strong> </a> Api または新しい<a href="https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-powersetrequest" data-raw-source="[&lt;strong&gt;PowerSetRequest function (Windows)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winbase/nf-winbase-powersetrequest)"> <strong>PowerSetRequest 関数 (Windows)</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerrequest" data-raw-source="[&lt;strong&gt;PoSetPowerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerrequest)"> <strong>PoSetPowerRequest</strong> </a> Api。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SystemAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元のシステム要求を許可するかどうかを報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元の表示要求を許可するかどうかを報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;AwayModeAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元の退席中モード要求を許可するかどうかを報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerfBoostAllowed&gt;</strong></td>
<td align="left"><p>この呼び出し元のパフォーマンス向上の要求を許可するかどうかを報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ExecutionRequiredAllowed&gt;</strong></td>
<td align="left"><p>実行では、この呼び出し元の要求を許可する必要かどうかを報告します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SystemCount&gt;</strong></td>
<td align="left"><p>この呼び出し元のシステム要求の数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DisplayCount&gt;</strong></td>
<td align="left"><p>この呼び出し元の表示要求の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AwayModeCount&gt;</strong></td>
<td align="left"><p>この呼び出し元の退席中モード要求の数。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PerfBoostCount&gt;</strong></td>
<td align="left"><p>この呼び出し元のパフォーマンス向上の要求の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ExecutionRequiredCount&gt;</strong></td>
<td align="left"><p>実行の数には、この呼び出し元の要求が必要です。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CreatePowerRequestEvent&gt;</strong></td>
<td align="left"><p>呼び出し元には、新しい要求が作成されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ChangePowerRequestEvent&gt;</strong></td>
<td align="left"><p>呼び出し元には、要求の数が変更されました。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ClosePowerRequestEvent&gt;</strong></td>
<td align="left"><p>呼び出し元には、要求が終了しました。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

[PowerCfg](https://go.microsoft.com/fwlink/p/?linkid=294568)

 

 






