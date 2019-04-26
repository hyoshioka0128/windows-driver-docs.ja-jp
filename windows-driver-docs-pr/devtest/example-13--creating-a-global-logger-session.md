---
title: 13 グローバル ロガー セッションの作成の例
description: 13 グローバル ロガー セッションの作成の例
ms.assetid: 11574df3-817e-4bf3-a849-dd5ac723fb1d
keywords:
- セッション WDK、グローバルのロガーをトレースします。
- グローバルなロガー トレース セッション WDK、例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42d62abc4e6f4866354fd253d3551805daecec2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344720"
---
# <a name="example-13-creating-a-global-logger-session"></a>例 13:グローバル ロガー セッションの作成


## <span id="ddk_controlling_a_global_logger_session_tools"></span><span id="DDK_CONTROLLING_A_GLOBAL_LOGGER_SESSION_TOOLS"></span>


A[グローバル ロガー トレース セッション](global-logger-trace-session.md)レジストリ エントリから構成パラメーターを読み取るその他のトレース セッションは異なります。 トレース ログがこれらの違いを処理するためのコマンドを起動し、グローバルのロガーのトレース セッションを停止するために使用しないでくださいと似ていますから他のセッションの。 ただし、グローバル ロガー セッションを更新することはできませんし、セッションの停止後に使用する必要があります、 **tracelog-削除**コマンド、セッションの作成、レジストリ エントリをリセットします。

また、 **tracelog-開始**コマンドは、トレース セッションを開始していない; だけに作成され構成されます。 セッションは、システムを再起動するときに起動します。

次のコマンドは、グローバル ログ セッションを構成する最も簡単なコマンドです。 使用して、 **tracelog-開始**コマンドと、予約済み**GlobalLogger**名。 トレース ログは、その他のすべてのパラメーターの既定値を使用します。

```
tracelog -start GlobalLogger
```

応答、トレース ログを作成、 **GlobalLogger**でサブキー **HKLM\\システム\\CurrentControlSet\\コントロール\\WMI**レジストリ エントリ各パラメーター。 作成されます、**開始**サブキーのエントリとその値に設定\`1。

コマンドが含まれていないため、 **-f**グローバル ロガー トレース セッションでは、%systemroot% パラメーターでは、このセッションのトレース ログが既定の場所に格納されている\\System32\\LogFiles\\WMI\\trace.log します。 ログを表示するには使用[Tracefmt](tracefmt.md)または[traceview で](traceview.md)、System.tmf で[トレース メッセージのフォーマット ファイル](trace-message-format-file.md)します。

セッションの構成後は、トレース セッションを開始するシステムを再起動します。

次のコマンドは、トレース セッションを停止しますが、レジストリ エントリには影響しません。

```
tracelog -stop GlobalLogger
```

次に、レジストリ エントリをリセットするには、次のコマンドを使用します。

```
tracelog -remove GlobalLogger
```

このコマンドは、省略可能なパラメーター (none、ここでは) のすべてのレジストリ エントリを削除します。 外に出て、 **GlobalLogger**サブキーと**開始**がエントリの値を設定します。**開始**0 (開始しないでください)。

**Tracelog-削除**コマンドは必要ありません。 レジストリのエントリのままにし、次回のグローバル ロガーのトレース セッションを実行するときに使用できます。 Tracelog によってレジストリ エントリの値で指定された値で置換パラメーターの異なるセッションを開始する場合、 **tracelog-開始**コマンド。

 

 





