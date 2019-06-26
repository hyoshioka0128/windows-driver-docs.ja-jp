---
title: PwrTest の構文
description: PwrTest をコマンド プロンプト ウィンドウから実行するとします。 選択し、PwrTest シナリオのコマンド オプションを使用して構成できます。
ms.assetid: bcae1bb6-ce5b-4ece-a5ba-bae6fefd6408
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e7482b861dd8130b203acdb5f739a11e25f1efc6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356401"
---
# <a name="pwrtest-syntax"></a>PwrTest の構文


PwrTest をコマンド プロンプト ウィンドウから実行するとします。 選択して構成できる[PwrTest シナリオ](pwrtest-scenarios.md)コマンド オプションを使用します。

PwrTest ツールの構文です。

```
pwrtest /scenario [/scenario_options] [/common_options]
```

<span id="_scenario"></span><span id="_SCENARIO"></span> **/** <em>シナリオ</em>  

| シナリオ   | 説明                                                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| sleep       | スリープ/再開の遷移を使用してコンピューターを循環します。 (Windows 7 以降)                                                                                        |
| バッテリ     | バッテリに関する情報と監視を提供します。 (Windows 7 以降)                                                                                                 |
| 情報        | システム電源の情報を提供します。 (Windows 7 以降)                                                                                                           |
| はい          | スレッドの実行状態モニター。 (Windows 7 以降)                                                                                                             |
| アイドル状態します。        | システムのアイドル状態のイベントを監視します。 (Windows 7 以降)                                                                                                                 |
| ppm         | プロセッサの電源管理を監視します。 (Windows 7 以降)                                                                                                         |
| タイマー       | システム タイマー精度変更を監視します。 (Windows 7 以降)                                                                                                    |
| ディスク        | 監視ディスクのアイドル状態の統計およびスピン ダウン イベント。 (Windows 7 以降)                                                                                          |
| デバイス      | モニターのデバイスのアイドル状態統計と電源イベント。 (Windows 7 以降)                                                                                       |
| モニター     | ユーザーのアイドル状態の自動暗転と非表示モニターに関連する統計情報を記録します。(Windows 7 以降)                                                            |
| requests    | 未処理と新しい電源の要求を表示します。 (Windows 7 以降)                                                                                                 |
| 温度     | モニターの ACPI 熱のゾーンの情報と統計情報。 これは、温度のゾーンと気温の変化を報告するシステムでのみサポートします。 (Windows から 7 以降)。 |
| processidle | 強制的にバック グラウンド メンテナンスでは、(ここではなく、スケジュールされた時刻) を実行するタスクおよびその進行状況を監視します。 (Windows 7 以降)                        |
| cs          | システムでサポートされている場合は、接続されているスタンバイ遷移を使用してコンピューターを循環します。 (Windows 8 以降)                                               |
| platidle    | 監視し、システムでサポートされている場合、プラットフォームのアイドル状態の遷移の数をログインしようとしています。 (Windows 8 以降)                                            |
| directedfx  | 監視に関連する低電力アイドル状態スイッチ[Directed 電源管理フレームワーク (DFx)](../kernel/introduction-to-the-directed-power-management-framework.md)します。 (Windows 10、バージョンが 1903 およびそれ以降)|


 


<span id="_scenario_options"></span><span id="_SCENARIO_OPTIONS"></span> **/** <em>シナリオ\_オプション</em>  
Pwrtest シナリオごとに使用できるオプションを参照する入力: **pwrtest.exe/** <em>シナリオ</em> **/でしょうか。**

例: **pwrtest.exe/sleep/でしょうか。**

<span id="_common_options"></span><span id="_COMMON_OPTIONS"></span>/*一般的な\_オプション*  

|       *一般的な\_オプション*       |                                                                                                                説明                                                                                                                 |
|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    **/lf:** <em>フォルダー</em>    |                                            ログ ファイルのフォルダーを指定します。 たとえば、c:\\myfolder または\\ \\server\\を共有します。 既定のログの場所は、pwrtest.exe と同じフォルダーです。                                             |
|     **/ln:** <em>name</em>     |                ログ ファイルの名前と、Event Tracing for Windows (ETW) トレース セッションの名前を指定します。 (.Wtl、.xml など)、ログ ファイルの拡張機能が自動的に追加されます。 既定の名前は pwrtestlog です。                |
| **/etwbuffersize:** <em>n</em> |                                                  既定のサイズよりも大きい場合は、(KB 単位)、ETW バッファーのサイズを指定します。 既定値は、現在のページ サイズまたは (大きい方) 256 KB です。                                                  |
| **/etwminbuffers:** <em>n</em> |                                論理プロセッサあたり 2 つの最小値よりも大きい場合は、ETW セッションに割り当てられたバッファーの最小数を指定します。 既定では論理プロセッサごとの 2 つのバッファーです。                                |
| **/etwmaxbuffers:** <em>n</em> | その数が 2 論理プロセッサごとの最小値よりも大きい場合に、ETW セッションに割り当てられたバッファーの数を超える最大値を指定します、 **etwminbuffers**設定します。 既定値は、 **etwminbuffers**値 + 20。 |
|        **/delaywrite**        |                                                           ログ データがディスク書き込み回数を削減するためのメモリにバッファリングされることを指定します。 このオプションでは、ETL を含むすべてのログの種類に影響します。                                                            |

**使用例**

```
pwrtest /?  
```

```
pwrtest /requests  /?
```

```
pwrtest /requests  /t:60
```

### <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈

ETW トレースをサポートするための要件を実行します。

-   Pwrtest をから管理者または管理者特権で実行する必要があります**コマンド プロンプト**ウィンドウ (**管理者として実行**)。

-   Pwrtest をネイティブに実行する必要があります (WoW64 はサポートされていません)。

システム管理者によって設定されたグループ ポリシー設定の影響は一時的に電源 (スリープ シナリオ) などの値の設定を変更する必要があるいくつかのシナリオにあります。

.Log (プレーン テキスト) で、各実行に対して複数のログを自動的に生成されます PwrTest .xml (形式は各シナリオは異なります)、.wtl (WTTLog) および .etl (ETW トレース) ログの形式。

PwrTest のすべてのシナリオを使用できるようにするには、まず Visual Studio と WDK を使用してテストするためのテスト コンピューターをプロビジョニングする必要があります。 詳細については、次を参照してください。[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)、または[ドライバーの展開のためにコンピューターをプロビジョニングし、テスト (WDK 8)](https://docs.microsoft.com/previous-versions/hh698272(v=vs.85))します。 一部のシナリオでは、Windows ドライバー テスト フレームワーク (WDTF) の一部である電源ボタン ドライバーが必要です。 WDTF (および、同梱の電源ボタン ドライバー) は、Visual Studio と WDK を使用してテストするためのシステムをプロビジョニングするときに自動的にインストールします。 WDTF については、次を参照してください。 [ **Windows デバイスのテスト フレームワーク (WDTF) (Windows ドライバー)** ](https://docs.microsoft.com/windows-hardware/drivers/wdtf/index)します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[PwrTest シナリオ](pwrtest-scenarios.md)

[PwrTest ログ ファイル](pwrtest-log-file.md)

 

 






