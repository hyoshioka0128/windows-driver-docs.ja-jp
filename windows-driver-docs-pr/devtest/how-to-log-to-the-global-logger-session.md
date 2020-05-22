---
title: グローバル ロガー セッションにログ記録する方法
description: グローバル ロガー セッションにログ記録する方法
ms.assetid: b5efea00-39cd-4df3-aac4-ade9126f69ed
keywords:
- グローバルロガートレースセッション WDK、ログ記録
- ブート時グローバルロガートレースセッション WDK、ログ記録
- ブート中に WDK トレースをログに記録します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173b851a9fad621d66b386396780be271a7282fe
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769712"
---
# <a name="how-to-log-to-the-global-logger-session"></a>グローバル ロガー セッションにログ記録する方法


グローバルロガートレースセッションにログを記録するようにドライバーを構成するには、次の手順に従います。

1. 次の定義をドライバーコードに追加します。 [WPP \_ コントロール \_ guid](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))マクロ定義と、[トレースメッセージヘッダーファイル](trace-message-header-file.md)の include ステートメントとの間に定義を挿入します。
   ```
   #define WPP_GLOBALLOGGER
   ```

2. [Tracelog](tracelog.md)を使用して、グローバルロガートレースセッションを構成します。 最も簡単なコマンドは次のとおりです。

   ```
   tracelog -start GlobalLogger
   ```

   グローバルロガートレースセッションを構成するためのパラメーターなど、完全な手順については、「 [**Tracelog コマンド構文**](tracelog-command-syntax.md)」と「[グローバルロガートレースセッション](global-logger-trace-session.md)」を参照してください。

   例については、「[例 13: グローバルロガーセッションの作成](example-13--creating-a-global-logger-session.md)」を参照してください。

   このコマンドでは、トレースセッションを作成して構成しますが、システムを再起動するまでセッションは開始されません (手順 5)。

3. **HKLM \\ System \\ CurrentControlSet \\ control \\ WMI \\ globallogger**サブキーの下に、トレースプロバイダーの[コントロール GUID](control-guid.md)として、という名前のサブキーを追加します。 Windows Vista 以降のバージョンの Windows では、コントロールの GUID は中かっこ () で囲む必要があり {} ます。

   **トレースログ start globallogger**コマンドは、 **globallogger**サブキーをレジストリに追加します。 **Controlguid**サブキーは、グローバルロガートレースセッションの[トレースプロバイダー](trace-provider.md)としてドライバーを確立します。

   たとえば、Windows XP を実行しているコンピューター上のグローバルロガートレースセッションにログを記録するように Tracedrv サンプルドライバーを構成するには、Tracedrv コントロール GUID (d58c126f-b309-11d1-969e-0000f875a5bc: **HKLM \\ SYSTEM \\ CurrentControlSet \\ control \\ WMI \\ globallogger \\ d58c126f-b309-11d1-969e-0000f875a5bc**) にという名前のサブキーを追加します。

   ソフトウェアトレース用に設計された[Tracedrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)は、GitHub の[Windows ドライバーサンプル](https://github.com/Microsoft/Windows-driver-samples)リポジトリで入手できます。

4. トレースプロバイダーを構成するには、次のレジストリエントリを**Controlguid**サブキーに追加します。 これらのエントリは省略可能で、値はドライバーによって定義されます。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">エントリ名</th>
   <th align="left">データ型</th>
   <th align="left">説明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>フラグ</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>プロバイダーの<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">トレースフラグ</a>を指定します。</p>
   <p>フラグの意味は、各トレースプロバイダーによって個別に定義されます。 通常、フラグは、より詳細なレポートレベルを表します。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>Level</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>プロバイダーの<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">トレースレベル</a>を指定します。</p>
   <p><strong>レベル</strong>値の意味は、各トレースプロバイダーによって個別に定義されます。 通常、トレースレベルは、イベントの重大度 (情報、警告、またはエラー) を表します。</p></td>
   </tr>
   </tbody>
   </table>




**Flags**エントリの名前が複数形で、**レベル**エントリの名前が単数形であることに注意してください。


5.  システムを再起動します。 これにより、グローバルロガートレースセッションが開始されます。

テストが完了したら、 **Controlguid**サブキーを削除するか、 **globallogger**サブキーの**開始**エントリの値を0に設定します。 そうしないと、システムを再起動するたびに、グローバル Logger セッションが実行され、ドライバーによってログに記録されます。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

WPP \_ globallogger が存在する場合、wpp は、レジストリを読み取り、グローバル logger セッションが実行されているかどうか、およびグローバル logger セッションのトレースに対してドライバーが有効になっているかどうかを判断するコードを追加します。 このコードは、ドライバーが標準のトレースセッションから受信する有効化通知の代わりに使用します。

また、グローバル Logger セッションはコールバック通知を提供しないため、Windows はコールバックが発生したと想定し、それに応じて処理を進めます。

WPP 定義によって生成されるコードの量はごくわずかであるため、テスト後にコードから削除する必要はありません。









