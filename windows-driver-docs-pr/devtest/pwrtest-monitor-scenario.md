---
title: PwrTest モニターのシナリオ
description: PwrTest モニターのシナリオでは、ユーザーのアイドル状態のモニターまたは表示の自動暗転と非表示に関連する統計情報を記録します。
ms.assetid: 8B45C85A-01E8-4256-82F3-097871CB9021
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a9e3a9b439f3888e05ffcbdee460e10f80462c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535337"
---
# <a name="pwrtest-monitor-scenario"></a>PwrTest モニターのシナリオ

PwrTest モニターのシナリオでは、ユーザーのアイドル状態のモニターまたは表示の自動暗転と非表示に関連する統計情報を記録します。

PwrTest モニターのシナリオを実行するときにも実行する場合、 [PwrTest 要求シナリオ](pwrtest-requests-scenario.md)(**要求/**) 別のウィンドウでのシナリオ。 PwrTest 要求シナリオは可能性がある場合でも、ユーザーは、期限切れにするには、アイドル状態のタイマーの十分な時間がアイドルにモニターにもまだ理由や、システムが起動状態を把握するのに役立ちます。

どちらのシナリオを実行する場合に使用することを確認して、 **/ln:**<em>名前</em>パラメーター変更できるように、ログ ファイルと ETW トレース セッションの名前。 名前は、ツールの 2 つのインスタンス間の競合を回避するために別にする必要があります。

## <a name="syntax"></a>構文

```command
pwrtest.exe /monitor  [/t:n] [/?] 
```

**/t:**<em>n</em>  
シナリオの実行を合計時間 (分) を指定します (既定値の*n*は 30 分です)。

### <a name="examples"></a>例

```command
pwrtest.exe /device 
```

```command
pwrtest.exe /device /t:60
```

### <a name="xml-log-file-output"></a>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <MonitorPower> 
    <PhysicalMonitorBrightnessEvent>
        <Timestamp></TimeStamp>
        <PhysicalMonitorBrightnessPercent></PhysicalMonitorBrightnessPercent>
    </PhysicalMonitorBrightnessEvent>
    <MonitorIdleStatusEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <AccruedIdleTimeMs></AccruedIdleTimeMs>
    </MonitorIdleStatusEvent>
    <MonitorTimeoutsChangeEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <DisplayTimeoutValueMs></DisplayTimeoutValueMs>
        <ScreenSaverTimeoutValueMs></ScreenSaverTimeoutValueMs>
        <DimTimeoutValueMs></DimTimeoutValueMs>
        <DimBrightnessValue></DimBrightnessValue>
        <NormalBrightnessValue></NormalBrightnessValue>
    </MonitorTimeoutsChangeEvent>
    <MonitorIdleActionExpireEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <IsConsoleSession></IsConsoleSession>
        <IdleAction></IdleAction>
        <IdleStartTime></IdleStartTime>
        <TimeoutValueMs></TimeoutValueMs>
    </MonitorIdleActionExpireEvent>
    <MonitorPowerEvent>
        <Timestamp></TimeStamp>
        <SessionId></SessionId>
        <IsConsoleSession></IsConsoleSession>
        <NewState></NewState>
        <PreviousState></PreviousState>
        <PreviousStateTime></PreviousStateTime>
    </MonitorPowerEvent>
    <MonitorAdaptiveDimTimeoutEvent>
        <Timestamp></TimeStamp>
        <Timeout></Timeout>
    </MonitorAdaptiveDimTimeoutEvent>
  </MonitorPower>
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
<td align="left"><strong>&lt;MonitorPower&gt;</strong></td>
<td align="left"><p>別のモニターの電源のすべてのイベントが含まれています。 1 つのみ<strong>&lt;MonitorPower&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;SessionId&gt;</strong></td>
<td align="left"><p>イベントは、ユーザー セッションの名前。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IsConsoleSession&gt;</strong></td>
<td align="left"><p>物理コンソール セッションが物理のモニターに接続されているかどうかを示しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PhysicalMonitorBrightnessEvent&gt;</strong></td>
<td align="left"><p>イベントでは、現在のモニターの明るさを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorIdleStatusEvent&gt;</strong></td>
<td align="left"><p>イベントは、ユーザーがアイドル状態を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;AccruedIdleTimeMs&gt;</strong></td>
<td align="left"><p>未収ユーザー (ミリ秒) のアイドル時間。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorTimeoutsChangeEvent&gt;</strong></td>
<td align="left"><p>イベントでは、現在のアイドル タイムアウトを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DisplayTimeoutValueMs&gt;</strong></td>
<td align="left"><p>表示には、ミリ秒単位のタイムアウト値が空白です。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ScreenSaverTimeoutValueMs&gt;</strong></td>
<td align="left"><p>画面のスクリーン セーバーのタイムアウト値 (ミリ秒単位) です。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;DimTimeoutValueMs&gt;</strong></td>
<td align="left"><p>Dim のタイムアウト値をミリ秒で表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;DimBrightnessValue&gt;</strong></td>
<td align="left"><p>Dim 状態のときに使用する明るさです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NormalBrightnessValue&gt;</strong></td>
<td align="left"><p>状態のときに使用する明るさです。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorIdleActionExpireEvent&gt;</strong></td>
<td align="left"><p>イベントは、アイドル タイムアウトに達したし、アクションの実行を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;IdleAction&gt;</strong></td>
<td align="left"><p>実行されたアクションについて説明します (スクリーン セーバー開始、コンソールがロックされているモニター dim、モニターの空白)。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;IdleStartTime&gt;</strong></td>
<td align="left"><p>このアイドル状態の開始時刻。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TimeoutValueMs&gt;</strong></td>
<td align="left"><p>ミリ秒単位でアイドル状態のタイムアウト値。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorPowerEvent&gt;</strong></td>
<td align="left"><p>イベントは、ディスプレイのアイドル タイムアウトに達したし、アクションの実行を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;NewState&gt;</strong></td>
<td align="left"><p>(オン/dim/オフ)、モニターの新しい状態。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;PreviousState&gt;</strong></td>
<td align="left"><p>以前の状態 (オン/dim/オフ)、モニターの。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PreviousStateTime&gt;</strong></td>
<td align="left"><p>以前の状態で費やされた時間。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;MonitorAdaptiveDimTimeoutEvent&gt;</strong></td>
<td align="left"><p>イベントは、アダプティブ dim タイムアウトが変更されたことを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;タイムアウト&gt;</strong></td>
<td align="left"><p>秒単位で新しいタイムアウト値。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[PwrTest 構文](pwrtest-syntax.md)
