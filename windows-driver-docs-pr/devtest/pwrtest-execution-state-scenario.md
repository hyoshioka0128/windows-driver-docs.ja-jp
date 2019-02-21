---
title: PwrTest 実行状態のシナリオ
description: PwrTest 実行状態のシナリオ (/es) のモニター スレッドの現在実行中のプロセスとサービスの状態の変更を実行します。
ms.assetid: 5470c99b-5780-486f-b36a-922fb821b7f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f321396beaddca43406e4c201840a24d5f29cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548995"
---
# <a name="pwrtest-execution-state-scenario"></a>PwrTest 実行状態のシナリオ


PwrTest 実行状態のシナリオ (**/es**) モニター スレッドの現在実行中のプロセスとサービスの状態の変更を実行します。

**注**  この PwrTest 実行状態のシナリオは、主にレガシ電源要求の Api を使用してアプリケーションの使用[ **SetThreadExecutionState 関数 (Windows)** ](https://msdn.microsoft.com/library/windows/desktop/aa373208)). 監視する新しい power を使用するアプリケーション要求 Api など[ **PowerSetRequest 関数 (Windows)** ](https://msdn.microsoft.com/library/windows/desktop/dd405534)を使用して、 [PwrTest 要求シナリオ](pwrtest-requests-scenario.md)代わりにします。

 

アプリケーションとサービス可能性があります一時的に、モニターなどの電源管理設定を上書きし、スリープのアイドル タイムアウトなどのスレッドの実行状態を変更することで。 PwrTest 実行状態のシナリオは、スレッドの実行状態を監視し、システム状態の変更をアプリケーションとサービスは、Win32 を使用して行った[ **SetThreadExecutionState 関数 (Windows)** ](https://msdn.microsoft.com/library/windows/desktop/aa373208).

使用することができます、 **/es**シナリオと共に[PwrTest アイドル シナリオ](pwrtest-idle-scenario.md)アプリケーションとアイドル状態に移行することから、モニターまたはシステムを妨げているサービスを識別できるようにします。

### <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文

```
pwrtest /es  [/t:n] [/stes:{y|n}] [/rss:{y|n}] [/sss:{y|n}] [/all] [/user] [/kernel] [/idle] [/?] 
```

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

<span id="_stes_yn"></span><span id="_STES_YN"></span>**/stes:**{**y**|**n**}  
指定するかどうか[ **SetThreadExecutionState** ](https://msdn.microsoft.com/library/windows/desktop/aa373208)イベントをログに記録する必要があります (**y** (はい) は、既定値)。

<span id="_rss_yn"></span><span id="_RSS_YN"></span>**/rss:**{**y**|**n**}  
指定するかどうか**RegisterSystemState**イベントをログに記録する必要があります (**y** (はい) は、既定値)。

<span id="_sss_yn"></span><span id="_SSS_YN"></span>**/sss:**{**y**|**n**}  
指定するかどうか**SetSystemState**イベントをログに記録する必要があります (**y** (はい) は、既定値)。

<span id="_all"></span><span id="_ALL"></span>**/all**  
すべてのイベントをログ記録することを指定します ([**SetThreadExecutionState**](https://msdn.microsoft.com/library/windows/desktop/aa373208)、 **RegisterSystemState**、 **SetSystemState**)。

<span id="_user"></span><span id="_USER"></span>**/user**  
すべてのユーザー イベントをログ記録することを指定します ([**SetThreadExecutionState**](https://msdn.microsoft.com/library/windows/desktop/aa373208))。

<span id="_kernel"></span><span id="_KERNEL"></span>**/kernel**  
カーネル モード イベントのみをログ記録することを指定します (**RegisterSystemState**、 **SetSystemState**)。

<span id="_idle"></span><span id="_IDLE"></span>**アイドル状態/**  
アイドル状態の統計情報を記録します。

**例**

```
pwrtest /es /all
```

```
pwrtest /es /user
```

```
pwrtest /es /kernel
```

```
pwrtest /es /kernel /sss:n
```

```
pwrtest /es /kernel /rss:n
```

```
pwrtest /es /kernel /rss:y /sss:n
```

```
pwrtest /es /sss:n
```

```
pwrtest /es /rss:n /sss:n
```

```
pwrtest /es /stes:n 
```

```
pwrtest /es /all /idle 
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <ExecutionState> 
    <EsChange> 
      <Time>XX:XX:XX</Time>
      <Process></Process>
        <RawState></RawState>
        <Continuous></Continuous>
        <System></System>
        <Display></Display>
        <AwayMode></AwayMode>
    </EsChange> 
    <EsChange> 
      <Time>XX:XX:XX</Time>
      <Process></Process>
        <RawState></RawState>
        <Continuous></Continuous>
        <System></System>
        <Display></Display>
        <AwayMode></AwayMode>
    </EsChange> 
  </ExecutionState>
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
<td align="left"><strong>&lt;ExecutionState&gt;</strong></td>
<td align="left"><p>実行状態のシナリオに関連する情報が含まれています。 1 つのみ<strong>&lt;ExecutionState&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EsChange&gt;</strong></td>
<td align="left"><p>含む 1 つのスレッドの実行状態変更イベントに関連する情報。 される<strong>&lt;EsChange&gt;</strong>要素。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;時間&gt;</strong></td>
<td align="left"><p>実行状態変更イベントが発生した時刻を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;プロセス&gt;</strong></td>
<td align="left"><p>実行状態の変更を要求するプロセスのイメージ ファイルへのパスを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;RawState&gt;</strong></td>
<td align="left"><p>要求の実行状態を示します。 これは EXECUTION_STATE 型の 32 ビット値です (Windows.h を参照してください)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;継続的です&gt;</strong></td>
<td align="left"><p>プロセスに継続的な (ES_CONTINUOUS) を実行状態の変更が要求されたかどうかを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;システム&gt;</strong></td>
<td align="left"><p>プロセスが使用可能な (ES_SYSTEM_REQUIRED) にするか、システムを要求された場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;表示&gt;</strong></td>
<td align="left"><p>プロセスが使用可能な (ES_DISPLAY_REQUIRED) かどうかを表示を要求された場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AwayMode&gt;</strong></td>
<td align="left"><p>あるプロセスの要求された退席中モードかどうか (ES_AWAYMODE_REQUIRED) が有効にした場合 (TRUE) を示します (FALSE)。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






