---
title: グローバルのロガーのセッションにログオンする方法
description: グローバルのロガーのセッションにログオンする方法
ms.assetid: b5efea00-39cd-4df3-aac4-ade9126f69ed
keywords:
- グローバルなロガー トレース セッション WDK、ログ記録
- 起動時のグローバル ログ トレース セッション WDK、ログ記録
- 起動中に WDK トレース ログに記録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3586e9ac23a2c38be1067a0a8520b2ac91b88bfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548745"
---
# <a name="how-to-log-to-the-global-logger-session"></a>グローバルのロガーのセッションにログオンする方法


グローバル ロガーのトレース セッションにログインするのにためのドライバーを構成するのにには、次の手順を使用します。

1. ドライバー コードには、次の定義を追加します。 挿入の間での定義、 [WPP\_コントロール\_GUID](https://msdn.microsoft.com/library/windows/hardware/ff556186)マクロ定義との include ステートメント、[トレース メッセージのヘッダー ファイル](trace-message-header-file.md)します。
   ```
   #define WPP_GLOBALLOGGER
   ```

2. 使用[Tracelog](tracelog.md)グローバル ロガーのトレース セッションを構成します。 最も簡単なコマンドは次のとおりです。

   ```
   tracelog -start GlobalLogger
   ```

   完全な手順については、グローバルのロガーのトレース セッションを構成するためのパラメーターを含むを参照してください[ **Tracelog コマンド構文**](tracelog-command-syntax.md)と[ロガー トレース セッションのグローバル](global-logger-trace-session.md)します。

   例については、次を参照してください。[例 13。ロガーがグローバル セッションを作成する](example-13--creating-a-global-logger-session.md)します。

   このコマンドは、作成し、トレース セッションを構成しますが、セッションは、(手順 5) システムを再起動するまでは開始されません。

3. 下、 **HKLM\\システム\\CurrentControlSet\\コントロール\\WMI\\GlobalLogger**サブキーに、という名前のサブキーを追加、 [GUIDの制御](control-guid.md)トレース プロバイダーの。 Windows Vista および以降のバージョンの Windows では、コントロールの GUID を中かっこで囲む必要があります ( {} )。

   **Tracelog-GlobalLogger 開始**コマンドを追加、 **GlobalLogger**レジストリ サブキー。 **ControlGUID**サブキーとしてドライバーを確立する、[トレース プロバイダー](trace-provider.md)グローバル ロガーのセッションをトレースします。

   たとえば、Windows XP を実行しているコンピューター上のグローバル ロガー トレース セッションにログオンする Tracedrv サンプル ドライバーを構成するには、Tracedrv コントロール GUID、d58c126f b309-11 d 0000f875a5bc 969e 1 という名前のサブキーを追加します。**HKLM\\システム\\CurrentControlSet\\コントロール\\WMI\\GlobalLogger\\d58c126f-b309-11d1-969e-0000f875a5bc**します。

   [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)、ソフトウェア トレースのように設計されたドライバーのサンプルが記載されて、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507 )GitHub リポジトリにあります。

4. トレース プロバイダーを構成するには、次のレジストリ エントリを追加、 **ControlGUID**サブキー。 これらのエントリは省略可能とその値はドライバーによって定義されます。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">エントリ名</th>
   <th align="left">データの種類</th>
   <th align="left">説明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><p><strong>フラグ</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>指定します、<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">トレース フラグ</a>プロバイダー。</p>
   <p>フラグの意味は、各トレース プロバイダーによって個別に定義されます。 通常、フラグは、しだいに詳細レポートのレベルを表します。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><p><strong>レベル</strong></p></td>
   <td align="left"><p>REG_DWORD</p></td>
   <td align="left"><p>指定します、<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">トレース レベル</a>プロバイダー。</p>
   <p>意味、<strong>レベル</strong>各トレース プロバイダーによって値が個別に定義されます。 通常、トレース レベルは、(情報、警告、またはエラー)、イベントの重大度を表します。</p></td>
   </tr>
   </tbody>
   </table>




注意の名前、**フラグ**エントリが複数形との名前、**レベル**エントリが単数形。


5.  システムを再起動します。 これは、グローバルのロガーのトレース セッションを開始します。

テストが完了したら、削除、 **ControlGUID**サブキーまたは値の設定、**開始**内のエントリ、 **GlobalLogger**サブキーを 0 にします。 そうでない場合、ロガーがグローバル セッションを実行し、ドライバーを記録、システムを再起動するたびにします。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

ときに WPP\_GLOBALLOGGER が存在する、WPP はレジストリを読み取り、ロガーがグローバル セッションが実行されているかどうかと、ロガーがグローバル セッションへのトレースのドライバーが有効になっているかどうかを決定するコードを追加します。 このコードは、標準のトレース セッションから受け取るドライバーを有効にする通知の行われます。

また、グローバル ロガー セッションから、コールバック通知が提供されないため、Windows とコールバックが発生し、それに応じて処理を仮定します。

WPP 定義は、テストした後、コードから削除する必要はありませんので、少量のコード、のみを生成します。









