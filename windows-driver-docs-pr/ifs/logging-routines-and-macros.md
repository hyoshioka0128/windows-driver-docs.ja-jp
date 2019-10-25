---
title: ログ記録用ルーチンとマクロ
description: ログ記録用ルーチンとマクロ
ms.assetid: 343605bc-7992-4e9c-a9af-f57bb958a38b
keywords:
- RDBSS WDK ファイルシステム、ログ記録
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、ログ記録
- WDK RDBSS のログ記録
- RDBSSLOG マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 849ade2630632c9629474431ad96c43470dd36ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841138"
---
# <a name="logging-routines-and-macros"></a>ログ記録用ルーチンとマクロ


## <span id="ddk_logging_functions_and_macros_if"></span><span id="DDK_LOGGING_FUNCTIONS_AND_MACROS_IF"></span>


RDBSS には、ログ記録用のルーチンが多数用意されています。 これらのログ記録機能は常に存在します。 RDBSSLOG マクロが定義されている場合は、チェックされたビルドでのログ呼び出しの生成が有効になります。 \_RDBSSLOG が設定されていない場合、ログ記録の呼び出しは無効になります。

ログルーチンは、循環バッファーに格納されているログレコードを作成します。 各レコードは、レコード記述子によって左右に境界されます。 このレコード記述子の長さは4バイトです。

次の表には、ログ記録ルーチンが含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o エラーログにエラーを記録するために呼び出されます。</p>
<p>このルーチンを直接呼び出すのではなく、 <strong>RxLogFailure</strong>または<strong>RxLogEvent</strong>マクロを使用することをお勧めします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithannotation)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o エラーログレコードを割り当て、ログレコードを入力して、このレコードを i/o エラーログに書き込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、i/o エラーログレコードを割り当て、ログレコードを入力して、このレコードを i/o エラーログに書き込みます。 このルーチンは、行番号と状態を、i/o エラーログレコードに格納されている生データバッファーにエンコードします。</p>
<p>このルーチンを直接呼び出すのではなく、 <strong>RxLogFailureWithBuffer</strong>マクロを使用することをお勧めします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>このルーチンは、書式指定文字列と可変数のパラメーターを受け取り、ログ記録が有効になっている場合、i/o エラーログエントリとして記録するための出力文字列を書式設定します。</p>
<p>このルーチンを直接呼び出すのではなく、 <strong>RxLog</strong>マクロを使用することをお勧めします。</p>
<p>このルーチンは、Windows Server 2003、Windows XP、および Windows 2000 の RDBSS のチェックされたビルドでのみ使用できます。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、前の表に示したルーチンを呼び出す rxlog と rxprocs のヘッダーファイルで定義されています。 これらのマクロは、通常、これらのルーチンを直接呼び出す代わりに使用されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">マクロ</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxLog</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェックされたビルドでは、このマクロは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a>ルーチンを呼び出します。</p>
<p>リテールビルドでは、このマクロは何も行いません。</p>
<p><strong>RxLog</strong>への引数は、ログ記録をオフにする必要がある場合に null 呼び出しに変換できるようにするために、追加のかっこのペアで囲む必要があることに注意してください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>、 <em>id</em>、 <em>EventId</em>、 <em>Status</em>)</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>、 <em>id</em>、 <em>EventId</em>、 <em>Status</em>)</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>,、" <em>"、"</em> <em>"、"</em><em>状態</em>"、"<em>バッファー</em>の長さ"、"<em>長さ</em>なし")</p></td>
<td align="left"><p>このマクロは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a>ルーチンを呼び出します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogRetail</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェックされたビルドでは、このマクロは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a>ルーチンを呼び出します。</p>
<p>リテールビルドでは、このマクロは何も行いません。</p>
<p><strong>RxLogRetail</strong>への引数は、ログ記録をオフにする必要がある場合に null 呼び出しに変換できるようにするために、追加のかっこのペアで囲む必要があることに注意してください。</p></td>
</tr>
</tbody>
</table>

 

 

 




