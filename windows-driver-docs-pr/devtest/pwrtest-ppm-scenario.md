---
title: PwrTest の PPM シナリオ
description: PwrTest PPM のシナリオでは、プロセッサの電源管理 (PPM) 情報および定期的な統計情報の合計を記録します。
ms.assetid: 735834dc-7351-44d1-a63f-9cb541184fde
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8596f134de9cf018fbc254fee0b7acab44d86749
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382694"
---
# <a name="pwrtest-ppm-scenario"></a>PwrTest の PPM シナリオ


PwrTest PPM のシナリオでは、プロセッサの電源管理 (PPM) 情報および定期的な統計情報の合計を記録します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /ppm [/n:n] [/i:n] [/c:[y|n]] [/p:{y|n}] [/u:{y|n}] [/live] [/t:n] [/?] 
```

<span id="_n_n"></span><span id="_N_N"></span>**/n:**<em>n</em>  
(既定値は 100) サイクルの数を指定します。 キーを押して**q**を終了する)。

<span id="_i_n"></span><span id="_I_N"></span>**/i:**<em>n</em>  
C 状態とプロセッサの使用率 (5000 ミリ秒は既定値) のポーリング間隔をミリ秒 (ms) を指定します。

<span id="_c_yn"></span><span id="_C_YN"></span>**c:**{**y**|**n**}  
かどうかを指定します C 状態情報をキャプチャする必要があります。 オプションを [はい] (**y**)、またはまったく (**n**)。 既定値は [はい] (**y**)。

<span id="_p_yn"></span><span id="_P_YN"></span>**/p:**{**y**|**n**}  
パフォーマンスやスロットルの状態情報をキャプチャするかどうかを指定します。 オプションを [はい] (**y**)、またはまったく (**n**)。 [はい] (**y**)、既定値です。

<span id="_u_yn"></span><span id="_U_YN"></span>**u:**{**y**|**n**}  
CPU 使用率情報をキャプチャするかどうかを指定します。 オプションを [はい] (**y**)、またはまったく (**n**)。 [はい] (**y**)、既定値です。

<span id="_live"></span><span id="_LIVE"></span>**ライブ/**  
プロセッサの電源管理イベントをリアルタイムで表示します (その他のオプションは使用できません)。

<span id="_t_n"></span><span id="_T_N"></span>**t:**<em>n</em>  
指定します、分単位での合計のランタイムを示します、 **live/** オプション (既定値は 30 になります)。

**使用例**

```
pwrtest /ppm /c:y /p:y /u:y /n:60 /i:1000
```

```
  pwrtest /ppm /c:n /p:n /u:y /n:3600 /i:1000
```

```
  pwrtest /ppm /live
```

```
  pwrtest /ppm /live /t:60
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <PPMScenario> 
    <ProcessorInformation> 
      <PerformanceStates> 
        <PerformanceState  
            number="0" 
            frequency="" 
            percentofmaxfrequency="" 
            type="" /> 
      </PerformanceStates> 
      <ProcessorName> </ProcessorName> 
      <InterfaceType> </InterfaceType> 
      <TransitionLatency units=""></TransitionLatency> 
    </ProcessorInformation> 
    <ProcessorTraces interval=""> 
      <Trace> 
        <CpuId></CpuId> 
        <ElapsedT></ElapsedT> 
        <CPUIdle></CPUIdle> 
        <PState></PState> 
        <Frequency></Frequency> 
        <PercentOfMax></PercentOfMax> 
        <PStateType></PStateType> 
        <COne></COne> 
        <CTwo></COne> 
        <CThree></CThree> 
      </Trace> 
    </ProcessorTraces> 
  </PPMScenario> 
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
<td align="left"><strong>&lt;PPMScenario&gt;</strong></td>
<td align="left"><p>PPM シナリオに関連する情報が含まれています。 1 つしかない<strong>&lt;SleepScenario&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessorInformation&gt;</strong></td>
<td align="left"><p>パフォーマンスとスロットル状態機能など、プロセッサの静的な属性に関連する情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PerformanceStates&gt;</strong></td>
<td align="left"><p>一覧を含む<strong>&lt;PerformanceState&gt;</strong>要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ProcessorName&gt;</strong></td>
<td align="left"><p>プロセッサのフレンドリ名を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;InterfaceType&gt;</strong></td>
<td align="left"><p>プロセッサの電源管理機能を Windows およびプラットフォーム間でやり取りするためのメカニズムを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;TransitionLatency&gt;</strong></td>
<td align="left"><p>パフォーマンスの状態を切り替えるときは、待機時間を示します。 属性が含まれますユニットには、通常はマイクロ秒 (マイクロ秒)</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ProcessorTraces&gt;</strong></td>
<td align="left"><p>一覧を含む<strong>&lt;トレース&gt;</strong>要素。 それぞれの間隔を示す間隔属性が含まれます<strong>&lt;トレース&gt;</strong>要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;トレース&gt;</strong></td>
<td align="left"><p>PwrTest を使用するコマンド オプションによって異なりますトレース情報が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CpuId&gt;</strong></td>
<td align="left"><p>プロセッサを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ElapsedT&gt;</strong></td>
<td align="left"><p>PwrTest (ミリ秒単位) が開始されてからの経過時間を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CPUIdle&gt;</strong></td>
<td align="left"><p>プロセッサのアイドル時間の割合を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;pState&gt;</strong></td>
<td align="left"><p>現在のプロセッサ パフォーマンスの状態を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;頻度&gt;</strong></td>
<td align="left"><p>メガヘルツ単位で現在のプロセッサ パフォーマンスの状態の実際の頻度を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PercentOfMax&gt;</strong></td>
<td align="left"><p>現在のパフォーマンスの状態の最大周波数の割合を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PStateType&gt;</strong></td>
<td align="left"><p>パフォーマンスの状態がパフォーマンスの状態 (1) またはスロットル状態 (0) かどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;COne&gt;</strong></td>
<td align="left"><p>C1 の CPU のアイドル状態に費やされた CPU のアイドル時間の割合を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;CTwo&gt;</strong></td>
<td align="left"><p>C2 CPU のアイドル状態に費やされた CPU のアイドル時間の割合を示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;CThree&gt;</strong></td>
<td align="left"><p>C3 の CPU のアイドル状態に費やされた CPU のアイドル時間の割合を示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






