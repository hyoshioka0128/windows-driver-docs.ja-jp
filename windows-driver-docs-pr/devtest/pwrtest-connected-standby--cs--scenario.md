---
title: PwrTest のコネクト スタンバイ シナリオ
description: PwrTest 接続スタンバイ シナリオ (/cs) コネクテッド スタンバイ遷移の自動テストが容易になります。
ms.assetid: 2601603D-F9AF-4DEB-9A1B-F5A091A51B2B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b4ceb6d2d251014680a863c05989766ce22696
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358246"
---
# <a name="pwrtest-connected-standby-scenario"></a>PwrTest のコネクト スタンバイ シナリオ


PwrTest 接続スタンバイ シナリオ ( **/cs**) コネクテッド スタンバイ遷移の自動テストが容易になります。

PwrTest では、PDC フェーズで進行状況をログ記録、システムでサポートされている場合、プラットフォームのアイドル状態の遷移の数をログインしようとします。 これは、システムが、アイドル状態の詳細なプラットフォームを入力する場合と、すべてのソフトウェア コンポーネントは、移行をブロックしている場合の診断に役立ちます。

このシナリオがテスト システムをサポートする必要があります、*常に常時接続されている*(SoC および ARM のほとんどのシステムは、これをサポート) (AoAc) 電源機能。 このシナリオでは、Windows ドライバー テスト フレームワーク (WDTF) の一部である電源ボタン ドライバーも必要です。 WDTF (および、同梱の電源ボタン ドライバー) は、Visual Studio と WDK を使用してテストするためのシステムをプロビジョニングするときに自動的にインストールします。 詳細については、次を参照してください。[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)、または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))します。 WDTF については、次を参照してください。 [ **Windows デバイスのテスト フレームワーク (WDTF) (Windows ドライバー)** ](https://docs.microsoft.com/windows-hardware/drivers/wdtf/index)します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


```
pwrtest /cs [/c:n] [/d:n] [/p:n][/?] 
```

<span id="_c_n"></span><span id="_C_N"></span> **/c:** <em>n</em>  
実行するには、(既定では 1) サイクルの数を指定します。

<span id="_d_n"></span><span id="_D_N"></span> **/d:** <em>n</em>  
遅延時間 (単位: 秒) には、スタンバイの遷移を (既定値は 60 秒です) 間接続されているを指定します。

<span id="_p_n"></span><span id="_P_N"></span> **/p:** <em>n</em>  
コネクテッド スタンバイの終了時刻を指定します (秒単位。 60 秒は既定値)。

**使用例**

```
pwrtest /cs /c:4 
```

```
pwrtest /cs /c:4 /p:120 /d:150
```

### <a name="span-idxmllogfileoutputspanspan-idxmllogfileoutputspanspan-idxmllogfileoutputspanxml-log-file-output"></a><span id="XML_log_file_output"></span><span id="xml_log_file_output"></span><span id="XML_LOG_FILE_OUTPUT"></span>XML ログ ファイルの出力

```XML
<PwrTestLog>
  <SystemInformation>
  </SystemInformation>
  <CSTransitions>
    <EnteringCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <InputDisabled Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <PhaseEnter name="name" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <PhaseExit name="name" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <ExitingCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/> || 
        <AbortingCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <InputEnabled Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <ExitedCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/> || 
        <AbortedCS Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <ExecutionRequiredSet Caller="c:\folder\process.exe" 
        Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/> ||
        <ExecutionRequiredCleared Caller="c:\folder\process.exe" 
            Timestamp="XX/XX/XXXX:XX:XX:XX.XXX"/>
    <PlatformIdleStats StateCount="X" Timestamp="XX/XX/XXXX:XX:XX:XX.XXX">
        <State Index="X" SuccessCount="X" FailureCount="X" CancelCount="X"/>
    </PlatformIdleStats>
  </CSTransitions>
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
<td align="left"><strong>&lt;CSTransitions&gt;</strong></td>
<td align="left"><p>すべての異なるコネクテッド スタンバイ イベントが含まれています。 1 つのみ<strong>&lt;CSTransitions&gt;</strong> PwrTest ログ ファイル内の要素。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;タイムスタンプ&gt;</strong></td>
<td align="left"><p>ある特定のイベントのタイムスタンプ。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;TemperatureScale&gt;</strong></td>
<td align="left"><p>温度単位 (華氏/ケルビン/(摂氏)&gt;のある特定のイベント。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ThermalZoneDeviceInstance&gt;</strong></td>
<td align="left"><p>ある特定のイベントの熱のゾーンのデバイスのインスタンス名。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;_TMP&gt;</strong></td>
<td align="left"><p>ある特定のイベントのシステムの現在の気温。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;_PSV&gt;、 &lt;_TCx&gt;、 &lt;_TSP&gt;、&lt;上昇して _ACx&gt;、 &lt;_HOT&gt;、 &lt;_CRT&gt;など。</strong></td>
<td align="left"><p>システム温度のしきい値は特定のイベントに送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PassiveCooling&gt;</strong></td>
<td align="left"><p>イベントは、システムが受動冷却のゾーンを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ActiveCooling&gt;</strong></td>
<td align="left"><p>イベントは、システムがアクティブな冷却ゾーンを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ホット&gt;</strong></td>
<td align="left"><p>イベントは、システムがホット トリップ ポイントをヒットを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;重要です&gt;</strong></td>
<td align="left"><p>イベントは、システムには、旅行の重要なポイントがヒットを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ActiveCoolingDevicePower&gt;</strong></td>
<td align="left"><p>イベントは、アクティブな冷却デバイスの電源がオンを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;FanDeviceInstance&gt;</strong></td>
<td align="left"><p>ファンのデバイスのインスタンス名。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;PowerState&gt;</strong></td>
<td align="left"><p>(1) またはオフ (0) の電源の状態。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>&lt;ActiveCoolingLevel&gt;</strong></td>
<td align="left"><p>アクティブな冷却の数値のレベルです。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>&lt;ActiveCoolingDeviceIndex&gt;</strong></td>
<td align="left"><p>冷却装置の数値インデックス。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest 構文](pwrtest-syntax.md)

 

 






