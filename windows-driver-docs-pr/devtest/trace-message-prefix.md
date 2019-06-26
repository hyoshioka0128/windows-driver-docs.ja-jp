---
title: トレース メッセージ プレフィックス
description: トレース メッセージ プレフィックス
ms.assetid: ab400174-cc2a-4cb8-9b7b-390af6464a2e
keywords:
- Tracefmt WDK、トレース メッセージのプレフィックス
- WDK Tracefmt プレフィックス
- トレース メッセージのプレフィックス WDK Tracefmt
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c60359392686143c65ded544b7fa32c96e602f0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379590"
---
# <a name="trace-message-prefix"></a>トレース メッセージ プレフィックス

Tracefmt を各トレース メッセージに格納されたデータで構成されるプレフィックスを追加する、[イベント トレース ログ (.etl) ファイル](trace-log.md)と[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)します。

Tracefmt には、既定では、特定のデータ要素が含まれていますが、ユーザーが追加および % のトレースを変更することで要素を削除\_形式\_プレフィックス環境変数、メッセージの定義との互換性を指定する文字列**FormatMessage**します。

既定のトレース メッセージのプレフィックスの形式は次のとおりです。

```command
[%9!d!]%8!04X!.%3!04X!::%4!s! [%1!s!]
```

これには、次のプレフィックスが生成されます。

```command
[CPUNumber]ProcessID.ThreadID :: SystemTime [MessageGUIDFriendlyName]
```

各 %*n*変数は、次の表で説明されているパラメーターを表します。

<table>
<thead>
<tr>
<th>変数の識別子をプレフィックスします。</th>
<th>変数の型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><p>%1</p></td>
<td><p>string</p></td>
<td><p>フレンドリ名、 <a href="message-guid.md" data-raw-source="[message GUID](message-guid.md)">GUID をメッセージ</a>のトレース メッセージ。 既定では、メッセージの GUID のフレンドリ名には、ディレクトリの名前、<a href="trace-provider.md" data-raw-source="[trace provider](trace-provider.md)">トレース プロバイダー</a>きました。</p>
<p>メッセージの GUID のフレンドリ名を変更するには、使用、 <strong>-p</strong> Tracewpp RUN_WPP マクロ パラメーター。 詳細については、Run_WPP オプションを参照してください。</p></td>
</tr>
<tr class="even">
<td><p>%2</p></td>
<td><p>string</p></td>
<td><p>ソース ファイルと行番号。</p>
<p>この変数は、トレース メッセージの表示名を表します。 既定では、トレース メッセージのフレンドリ名は、ソース ファイルとトレース メッセージを生成したコードの行番号の名前が。</p></td>
</tr>
<tr>
<td><p>%3</p></td>
<td><p>ULONG</p></td>
<td><p>スレッド id です。</p>
<p>トレース メッセージを生成したスレッドを識別します。</p></td>
</tr>
<tr class="even">
<td><p>%4</p></td>
<td><p>string</p></td>
<td><p>トレース メッセージが生成された時刻のタイムスタンプ。</p></td>
</tr>
<tr>
<td><p>%5</p></td>
<td><p>string</p></td>
<td><p>カーネル時間。</p>
<p>トレース メッセージが生成された時点で、CPU のティック単位で、カーネル モード命令の実行の経過時間を表示します。</p></td>
</tr>
<tr class="even">
<td><p>%6</p></td>
<td><p>string</p></td>
<td><p>ユーザーの時間です。</p>
<p>トレース メッセージが生成された時点で、CPU のティック単位でユーザー モードについては、実行の経過時間を表示します。</p></td>
</tr>
<tr>
<td><p>%7</p></td>
<td><p>LONG</p></td>
<td><p>シーケンス番号。</p>
<p>トレース メッセージのローカルまたはグローバルのシーケンス番号が表示されます。 このトレース セッションにのみ一意ではローカルのシーケンス番号は、既定値です。</p></td>
</tr>
<tr class="even">
<td><p>%8</p></td>
<td><p>ULONG</p></td>
<td><p>プロセス id です。</p>
<p>トレース メッセージを生成したプロセスを識別します。</p></td>
</tr>
<tr>
<td><p>%9</p></td>
<td><p>ULONG</p></td>
<td><p>CPU の数。</p>
<p>トレース メッセージが生成された CPU を識別します。</p></td>
</tr>
<tr class="even">
<td><p>%!FUNC!</p></td>
<td><p>string</p></td>
<td><p>関数の名前。</p>
<p>トレース メッセージを生成した関数の名前が表示されます。</p></td>
</tr>
<tr>
<td><p>%!フラグ。</p></td>
<td><p>string</p></td>
<td><p>名前を表示、<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">トレース フラグ</a>トレース メッセージを有効にします。</p>
<p>(ため、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"> <strong>DoTraceMessage</strong> </a>マクロ フラグとレベルの引数を逆に、DoTraceMessage によって生成されたメッセージの値を表示する、<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">トレース レベル</a>このフィールドに.)</p></td>
</tr>
<tr class="even">
<td><p>%!レベル。</p></td>
<td><p>string</p></td>
<td><p>値を表示、<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">トレース レベル</a>トレース メッセージをできるようにします。</p>
<p>(ため、 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85)" data-raw-source="[&lt;strong&gt;DoTraceMessage&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))"> <strong>DoTraceMessage</strong> </a>マクロ フラグとレベルの引数を逆に、DoTraceMessage によって生成されたメッセージの名前を表示する、<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">トレース フラグ</a>このフィールドにします)。</p></td>
</tr>
<tr>
<td><p>%!COMPNAME!</p></td>
<td><p>string</p></td>
<td><p>コンポーネントの名前。</p>
<p>トレース メッセージを生成したプロバイダーのコンポーネントの名前が表示されます。 コンポーネント名では、トレース コードで指定されている場合にのみ表示されます。</p></td>
</tr>
<tr class="even">
<td><p>%!SUBCOMP!</p></td>
<td><p>string</p></td>
<td><p>サブコンポーネントの名前。</p>
<p>トレース メッセージを生成したプロバイダーのサブコンポーネントの名前が表示されます。 コンポーネント名では、トレース コードで指定されている場合にのみ表示されます。</p></td>
</tr>
</tbody>
</table>

 

内の感嘆符シンボルは、書式設定と、変数の有効桁数を指定する変換の文字です。 たとえば、%8! 04 X! 4 桁の符号なし 16 進数として表されるプロセス ID を指定します。 これらの変換の文字を含める必要があります。

要素を変更する順序、またはトレース メッセージのプレフィックスの書式設定を使用してトレース %\_形式\_%path% 環境変数のプレフィックス。 例については、次を参照してください。[例 7。トレース メッセージのプレフィックスをカスタマイズする](example-7--customizing-the-trace-message-prefix.md)します。

TMF ファイルの内容の例は、tracedrv サンプルからのトレース メッセージの書式設定を参照してください。

また、 **csv**パラメーターを標準 Tracefmt プレフィックスの前に各トレース メッセージを構成できない、詳細なプレフィックスを追加します。 CSV のプレフィックス内のフィールドの説明は、使用、 **- csvheader**パラメーター。

 

 





