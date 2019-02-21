---
title: 書式指定文字列を拡張、WPP とは
description: 書式指定文字列を拡張、WPP とは
ms.assetid: f05117c0-cb4b-483a-a141-08423555170a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44b4ee86a2d9ac5c93c9df135032aa5f19b59856
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558322"
---
# <a name="what-are-the-wpp-extended-format-specification-strings"></a>書式指定文字列を拡張、WPP は何ですか。


WPP にはトレース メッセージに対して定義されている標準書式指定文字列のほかに使用できる定義済みの書式指定文字列が含まれます**printf**します。

使用することができます、 **% です。フラグ。**, **%!FUNC!** **% です。レベル。** 文字列を[トレース メッセージのプレフィックス](trace-message-prefix.md)、および任意のトレース関数またはマクロでなど[ **DoTraceMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544918)します。

すべてのトレース関数では、その他の拡張文字列を使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">書式指定文字列</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">ソフトウェア トレース</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%!ファイル。</p></td>
<td align="left"><p>トレース メッセージの生成元のソース ファイルの名前を表示します。 この変数でも使用できます、<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">トレース メッセージのプレフィックス</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!フラグ。</p></td>
<td align="left"><p>値を表示、<a href="trace-flags.md" data-raw-source="[trace flags](trace-flags.md)">トレース フラグ</a>トレース メッセージを有効にします。 この変数でも使用できます、<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">トレース メッセージのプレフィックス</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!FUNC!</p></td>
<td align="left"><p>トレース メッセージを生成した関数が表示されます。 この変数でも使用できます、<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">トレース メッセージのプレフィックス</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!レベル。</p></td>
<td align="left"><p>名前を表示、<a href="trace-level.md" data-raw-source="[trace level](trace-level.md)">トレース レベル</a>トレース メッセージをできるようにします。 この変数でも使用できます、<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">トレース メッセージのプレフィックス</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!行があります。</p></td>
<td align="left"><p>トレースのプレフィックスが生成されるコードで、行の行番号を表示します。 この変数でも使用できます、<a href="trace-message-prefix.md" data-raw-source="[trace message prefix](trace-message-prefix.md)">トレース メッセージのプレフィックス</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left">一般的な用途</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>% です。 ブール値。</p></td>
<td align="left"><p>TRUE または FALSE が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%! irql!</p></td>
<td align="left"><p>現在の IRQL の名前が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%! sid。</p></td>
<td align="left"><p>セキュリティ識別子 (pSID) へのポインターを表します。 SID を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!SRB!</p></td>
<td align="left"><p>SCSI 要求のブロックへのポインターを表します。 ブロックの内容を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!なるでしょう。</p></td>
<td align="left"><p>SCSI SENSE_DATA にポインターを表します。 検出データを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left">GUID</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%!GUID。</p></td>
<td align="left"><p>GUID (pGUID) へのポインターを表します。 指す GUID が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!CLSID。</p></td>
<td align="left"><p>クラスの id。 クラス ID の GUID にポインターを表します。 関連付けられた GUID の文字列が表示されます。 WPP は、トレース メッセージをフォーマットするときに、レジストリの文字列を検索します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!IID。</p></td>
<td align="left"><p>インターフェイス id です。 インターフェイス ID の GUID へのポインターを表します。 関連付けられた GUID の文字列が表示されます。 WPP は、トレース メッセージをフォーマットするときに、レジストリの文字列を検索します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!LIBID。</p></td>
<td align="left"><p>タイプ ライブラリ。 COM タイプ ライブラリの GUID を表します。 関連付けられた GUID の文字列が表示されます。 WPP は、トレース メッセージをフォーマットするときに、レジストリの文字列を検索します。</p></td>
</tr>
<tr class="even">
<td align="left">時間</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>%! デルタ!</p></td>
<td align="left"><p>(ミリ秒単位) の 2 つの時刻値の差を表示します。 表示される LONGLONG 値<strong>日 ~ h<span class="emoji" shortCode="m">Ⓜ️</span>s</strong>形式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!待機時間。</p></td>
<td align="left"><p>(ミリ秒単位) を完了するを待つに費やされた時間を表示します。 表示される LONGLONG 値<strong>日 ~ h<span class="emoji" shortCode="m">Ⓜ️</span>s</strong>形式。</p>
<p>使用するように設計<strong>%! due!</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%! 期限。</p></td>
<td align="left"><p>時間 (ミリ秒単位)、完了する予定は何かを表示します。 表示される LONGLONG 値<strong>日 ~ h<span class="emoji" shortCode="m">Ⓜ️</span>s</strong>形式。</p>
<p>使用するように設計<strong>% です。待機時間。</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!タイムスタンプ。</p>
<p>% です。 datetime。</p>
<p>%! 時間。</p></td>
<td align="left"><p>特定の時点でのシステム時刻の値を表示します。 これらは LARGE_INTEGER 値を SYSTEMTIME 形式で表示されます。</p>
<p>プログラムでさまざまな時間値を表すと、それらの間で区別する、これらの変数を使用することができます。</p></td>
</tr>
<tr class="odd">
<td align="left">リターン コード</td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>%!状態です。</p></td>
<td align="left"><p>状態値を表し、状態コードに関連付けられている文字列を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!WINERROR!</p></td>
<td align="left"><p>Windows のエラー コードを表し、エラーに関連付けられている文字列を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!HRESULT。</p></td>
<td align="left"><p>エラーまたは警告を表し、HRESULT の形式でコードを表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!NTerror!</p></td>
<td align="left"><p>Windows エラーを表し、エラー メッセージ文字列を表示します。</p></td>
</tr>
<tr class="even">
<td align="left">ネットワーク</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>%!IPADDR!</p></td>
<td align="left"><p>IP アドレスにポインターを表します。 IP アドレスが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>%!ポート。</p></td>
<td align="left"><p>ポート番号を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>%!NETEVENT!</p></td>
<td align="left"><p>ネットワーク イベントを表示します。</p></td>
</tr>
</tbody>
</table>

 

 

 





