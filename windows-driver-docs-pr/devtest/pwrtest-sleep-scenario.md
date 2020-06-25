---
title: PwrTest のスリープ シナリオ
description: PwrTest Sleep シナリオでは、スリープ状態の自動テストと遷移の再開が容易になります。
ms.assetid: 2003ff3e-bc29-4741-a0a6-371948982679
ms.date: 06/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9012fd4f3ccf85a843276e0b41db6aa72308fcdf
ms.sourcegitcommit: 0683ff4538df778e6890d073de23fc9e816f7899
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85334983"
---
# <a name="pwrtest-sleep-scenario"></a>PwrTest のスリープ シナリオ


PwrTest Sleep シナリオでは、スリープ状態の自動テストと遷移の再開が容易になります。

PwrTest は、自動化された方法でプラットフォームを1つまたは複数のスリープ状態にし、BIOS 初期化や合計再開時間などのスリープ状態のパフォーマンス情報をログに記録できるようにします。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


```
pwrtest /sleep [/c:n] [/d:n] [/p:n] [/h:{y|n}] [/s:{1|3|4|all|rnd|hibernate|standby|dozes4}] [/unattend] [dt:n] [/e:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c:**<em>n</em>  
実行するサイクル数 (既定値は 1) を指定します。

<span id="_d_n"></span><span id="_D_N"></span>**/d:**<em>n</em>  
遅延時間を秒単位で指定します (既定値は 90)。

<span id="_p_n"></span><span id="_P_N"></span>**/p:**<em>n</em>  
スリープ時間を秒単位で指定します (60 は既定値です)。 ウェイクタイマーが休止状態でサポートされていない場合は、システムが再起動され、休止状態ファイルの書き込み後すぐに再開されます)。

<span id="_h_yn"></span><span id="_H_YN"></span>**/h:**{**y** | **n**}  
ハイブリッドスリープを有効にするか (y)、無効にするかを指定します (n)。 既定値は [システムポリシーです。

<span id="_s_134allrndhibernatestandby"></span><span id="_S_134ALLRNDHIBERNATESTANDBY"></span>**/s:**{**1** | **3** | **4** | **all** | **rnd** | **休止状態**の | **スタンバイ** | **dozes4**}  

<span id="1"></span>**1**  
対象の状態が常に S1 であることを指定します。

<span id="3"></span>**番**  
対象の状態が常に S3 であることを指定します。

<span id="4"></span>**4/4**  
ターゲットの状態が常に S4 であることを指定します。

<span id="all"></span><span id="ALL"></span>**すべての**  
サポートされているすべての電源状態を順番に繰り返すように指定します。

<span id="rnd"></span><span id="RND"></span>**rnd**  
サポートされているすべての電源状態をランダムに循環するように指定します。

<span id="hibernate"></span><span id="HIBERNATE"></span>**解除**  
ターゲットの状態が常に休止状態 (S4) であることを指定します。

<span id="standby"></span><span id="STANDBY"></span>**standby**  
ターゲットの状態が任意の使用可能なスタンバイ状態 (S1 または S3) であることを指定します。

<span id="standby"></span><span id="STANDBY"></span>**dozes4**  
最新のスタンバイ (S0 低電力アイドル) から S4 に doze するように指定します。

<span id="_unattend____"></span><span id="_UNATTEND____"></span>**/unattend**   
ウェイクアップ後にシステム実行状態を変更しないように指定します。

<span id="_dt_n"></span><span id="_DT_N"></span>**/dt:**<em>n</em>  
DozeS4 のみの場合は、休止状態 (S4) に移行する前に、最新のスタンバイに使用する doze タイムアウトを秒単位で指定します。

<span id="_e_n"></span><span id="_E_N"></span>**/e:**<em>n</em>  
遷移終了イベントを待機するタイムアウト (秒) を指定します (既定値は120秒)。

**使用例**

```
pwrtest /sleep /c:4 /s:all 
```

```
pwrtest /sleep /c:4 /p:120 /d:150 /s:all
```

```
pwrtest /sleep /c:10 /s:dozes4 /dt:100 /p:100
```

### <a name="span-idxml_log_file_outputspanspan-idxml_log_file_outputspanspan-idxml_log_file_outputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <SleepScenario> 
    <SleepTransitions 
            critical="" 
            hybrid="" 
            delay="" 
            sleeptime=""> 
            <SleepTransition 
                  number="" 
                  status=""> 
                  <StartT></StartT> 
                  <EndT></EndT> 
                  <SleepTimeMs></SleepTimeMs> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInitTimeMs></BIOSInitTimeMs> 
                  <DriverWakeTimeMs></DriverWakeTimeMs> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberReadTimeMs></HiberReadTimeMs> 
                  <HiberWriteTimeMs></HiberWriteTimeMs> 
                  <HiberPagesWritten></HiberPagesWritten> 
            </SleepTransition> 
            <SleepTransition 
                  number="" 
                  status=""> 
                  <StartT></StartT> 
                  <EndT></EndT> 
                  <SleepTimeMs></SleepTimeMs> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInitTimeMs></BIOSInitTimeMs> 
                  <DriverWakeTimeMs></DriverWakeTimeMs> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberReadTimeMs></HiberReadTimeMs> 
                  <HiberWriteTimeMs></HiberWriteTimeMs> 
                  <HiberPagesWritten></HiberPagesWritten> 
            </SleepTransition>
    </SleepTransitions> 
  </SleepScenario> 
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
<td align="left"><strong>&lt;SleepScenario&gt;</strong></td>
<td align="left"><p>スリープシナリオに関連する情報が含まれています。 PwrTest ログファイルには、 <strong> &lt; SleepScenario &gt; </strong>要素が1つだけあります。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTransitions&gt;</strong></td>
<td align="left"><p>は、重要なスリープ機能やハイブリッドスリープ機能の状態など、スリープ切り替えサイクルに関する全体的なデータを提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SleepTransition&gt;</strong></td>
<td align="left"><p>開始時刻や終了時刻などのスリープごとのサイクル情報に加え、BIOS の初期化時間などの再開時間の詳細も提供します。 <strong> &lt; SleepTransition &gt; </strong>要素は、各スリープ遷移サイクルに対して生成されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;StartT&gt;</strong></td>
<td align="left"><p>スリープサイクルの開始時刻を示します。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EndT&gt;</strong></td>
<td align="left"><p>スリープサイクルの終了時刻を示します。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTimeMs&gt;</strong></td>
<td align="left"><p>スリープサイクルの期間を示します。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TargetState&gt;</strong></td>
<td align="left"><p>ターゲットのスリープ状態を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;効率のよい資産&gt;</strong></td>
<td align="left"><p>有効なスリープ状態を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BIOSInitTimeMs&gt;</strong></td>
<td align="left"><p>再開時に BIOS を初期化するのに必要な時間をミリ秒単位で示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DriverWakeTimeMs&gt;</strong></td>
<td align="left"><p>再開時にドライバーを初期化するのに必要な時間をミリ秒単位で示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;中断&gt;</strong></td>
<td align="left"><p>システムを中断するのに必要な時間をミリ秒単位で示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;Resume&gt;</strong></td>
<td align="left"><p>システムを再開するのに必要な合計時間をミリ秒単位で示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberReadTimeMs&gt;</strong></td>
<td align="left"><p>休止状態ファイルを読み取るために必要な時間をミリ秒単位で示します。 (TargetState は4である必要があります)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;HiberWriteTimeMs&gt;</strong></td>
<td align="left"><p>休止状態ファイルの書き込みに必要な時間をミリ秒単位で示します。 (有効にする必要があるのは 4)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberPagesWritten&gt;</strong></td>
<td align="left"><p>休止状態ファイルに書き込まれたページ数。 (有効にする必要があるのは 4)</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest の構文](pwrtest-syntax.md)










