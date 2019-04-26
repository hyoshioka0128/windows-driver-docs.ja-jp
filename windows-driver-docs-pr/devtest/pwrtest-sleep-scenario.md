---
title: PwrTest のスリープ シナリオ
description: PwrTest スリープ シナリオでは、スリープと復帰の遷移の自動テストが容易になります。
ms.assetid: 2003ff3e-bc29-4741-a0a6-371948982679
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef839a284e51312cc828c5653d3a5bfdb950a46
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360094"
---
# <a name="pwrtest-sleep-scenario"></a>PwrTest のスリープ シナリオ


PwrTest スリープ シナリオでは、スリープと復帰の遷移の自動テストが容易になります。

PwrTest は、プラットフォームを自動で 1 つまたは複数のスリープ状態に転送することと、BIOS の初期化と合計時間を再開するなど、スリープ状態のパフォーマンス情報が記録されます。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /sleep [/c:n] [/d:n] [/p:n] [/h:{y|n}] [/s:{1|3|4|all|rnd|hibernate|standby}] [/unattend] [/e:n] [/?] 
```

<span id="_c_n"></span><span id="_C_N"></span>**/c:**<em>n</em>  
実行するには、(1 は、既定値) のサイクル数を指定します。

<span id="_d_n"></span><span id="_D_N"></span>**/d:**<em>n</em>  
秒 (既定では 90) では、遅延時間を指定します。

<span id="_p_n"></span><span id="_P_N"></span>**/p:**<em>n</em>  
秒 (60 は既定値) では、スリープ時間を指定します。 ウェイク アップ タイマーが休止状態のサポートされていない場合、システムが再起動してすぐに再開休止状態ファイルを作成した後)。

<span id="_h_yn"></span><span id="_H_YN"></span>**h:**{**y**|**n**}  
ハイブリッド スリープを有効になっている (y) または (n) を無効にするかどうかを指定します。 既定値は、システム ポリシーです。

<span id="_s_134allrndhibernatestandby"></span><span id="_S_134ALLRNDHIBERNATESTANDBY"></span>**/s:**{**1**|**3**|**4**|**すべて**| **rnd**|**休止**|**スタンバイ**}  

<span id="1"></span>**1**  
対象の状態は S1 では常を指定します。

<span id="3"></span>**3**  
対象の状態が S3 では常を指定します。

<span id="4"></span>**4**  
対象の状態は、S4 では常を指定します。

<span id="all"></span><span id="ALL"></span>**すべての**  
順序ですべてのサポートされている電源状態の繰り返しを指定します。

<span id="rnd"></span><span id="RND"></span>**Rnd 関数**  
すべてのサポートされている電源状態をランダムに繰り返しを指定します。

<span id="hibernate"></span><span id="HIBERNATE"></span>**休止状態します。**  
対象の状態は休止状態常に (S4) を指定します。

<span id="standby"></span><span id="STANDBY"></span>**スタンバイ**  
対象の状態が利用可能なスタンバイ状態 (S1 または S3) であることを指定します。

<span id="_unattend____"></span><span id="_UNATTEND____"></span>**/unattend**   
ウェイク アップの後にシステムの実行状態を変更しないように指定します。

<span id="_e_n"></span><span id="_E_N"></span>**/e:**<em>n</em>  
移行の終了イベントを待機する秒単位のタイムアウトを指定します (既定では 120 秒)。

**使用例**

```
pwrtest pwrtest /sleep /c:4 /s:all 
```

```
  pwrtest /sleep /c:4 /p:120 /d:150 /s:all
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

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
                  <Duration></Duration> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInit></BIOSInit> 
                  <DriverInit></DriverInit> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberRead></HiberRead> 
                  <HiberWrite></HiberWrite> 
            </SleepTransition> 
            <SleepTransition 
                  number="" 
                  status=""> 
                  <StartT></StartT> 
                  <EndT></EndT> 
                  <Duration></Duration> 
                  <TargetState></TargetState> 
                  <EffectiveState></EffectiveState> 
                  <BIOSInit></BIOSInit> 
                  <DriverInit></DriverInit> 
                  <Suspend></Suspend> 
                  <Resume></Resume> 
                  <HiberRead></HiberRead> 
                  <HiberWrite></HiberWrite> 
            </SleepTransition> 
    </SleepTransitions> 
  </SleepScenario> 
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
<td align="left"><strong>&lt;SleepScenario&gt;</strong></td>
<td align="left"><p>スリープ シナリオに関連する情報が含まれています。 1 つしかない<strong>&lt;SleepScenario&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;SleepTransitions&gt;</strong></td>
<td align="left"><p>スリープの移行サイクルの重大な状態などに関する全体的なデータとハイブリッド スリープ機能を提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SleepTransition&gt;</strong></td>
<td align="left"><p>BIOS の初期化時など、再開時間について、開始と終了時刻、ほかの詳細などのスリープあたりサイクルについて説明します。 A <strong>&lt;SleepTransition&gt;</strong>スリープの移行サイクルごとに要素が生成されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;StartT&gt;</strong></td>
<td align="left"><p>スリープのサイクルの開始時刻を示します。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;EndT&gt;</strong></td>
<td align="left"><p>スリープのサイクルの終了時刻を示します。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;期間&gt;</strong></td>
<td align="left"><p>スリープのサイクルの期間を示します。 (<em>hh</em>:<em>mm</em>:<em>ss</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TargetState&gt;</strong></td>
<td align="left"><p>ターゲットのスリープ状態を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;EffectiveState&gt;</strong></td>
<td align="left"><p>有効なスリープ状態を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;BIOSInit&gt;</strong></td>
<td align="left"><p>BIOS を初期化するために必要な時間の量を示します (TargetState が 3 である必要があります) (ミリ秒単位) で再開します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DriverInit&gt;</strong></td>
<td align="left"><p>ミリ秒単位の再開時にドライバーを初期化するために必要な時間の量を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;中断&gt;</strong></td>
<td align="left"><p>時間 (ミリ秒単位)、システムを中断するために必要な数を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;再開&gt;</strong></td>
<td align="left"><p>ミリ秒単位でシステムを再開するために必要な時間の合計を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;HiberRead&gt;</strong></td>
<td align="left"><p>ミリ秒単位で休止状態ファイルの読み取りに必要な時間を示します。 (TargetState が 4 である必要があります)</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;HiberWrite&gt;</strong></td>
<td align="left"><p>ミリ秒単位で休止状態ファイルを書き込むために必要な時間を示します。 (EffectiveState が 4 である必要があります)</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)










