---
title: ログ記録ルーチンとマクロ
description: ログ記録ルーチンとマクロ
ms.assetid: 343605bc-7992-4e9c-a9af-f57bb958a38b
keywords:
- RDBSS WDK ファイル システムでは、ログ記録
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、ログ記録
- WDK RDBSS のログ記録
- RDBSSLOG マクロ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 686a8a93e2190d0a347746876f4862629ad4a7e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550600"
---
# <a name="logging-routines-and-macros"></a>ログ記録ルーチンとマクロ


## <span id="ddk_logging_functions_and_macros_if"></span><span id="DDK_LOGGING_FUNCTIONS_AND_MACROS_IF"></span>


RDBSS は、ログ記録のさまざまなルーチンを提供します。 これらのログ記録機能は、常に存在します。 RDBSSLOG マクロが定義されている場合、世代のチェック ビルドでログ記録の呼び出しは有効です。 ない場合\_RDBSSLOG が設定されている、ロギング呼び出しは無効になります。

ログ記録ルーチンでは、循環バッファーに格納されているログ レコードを作成します。 各レコードは、いずれかの側レコード記述子によって制限されます。 このレコードの記述子は、4 バイトです。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"><strong>RxLogEventDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O エラー ログにエラーをログに呼び出されます。</p>
<p>推奨されます、 <strong>RxLogFailure</strong>または<strong>RxLogEvent</strong>このルーチンを直接呼び出す代わりにマクロを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554519" data-raw-source="[&lt;strong&gt;RxLogEventWithAnnotation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554519)"><strong>RxLogEventWithAnnotation</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O エラーのログ レコードを割り当て、ログ レコードには、入力され、I/O エラー ログにこのレコードを書き込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554524" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554524)"><strong>RxLogEventWithBufferDirect</strong></a></p></td>
<td align="left"><p>このルーチンは、I/O エラーのログ レコードを割り当て、ログ レコードには、入力され、I/O エラー ログにこのレコードを書き込みます。 このルーチンは、I/O エラーのログ レコードに格納されている生データのバッファーに行番号と状態をエンコードします。</p>
<p>推奨されます、 <strong>RxLogFailureWithBuffer</strong>このルーチンを直接呼び出す代わりにマクロを使用します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"><strong>_RxLog</strong></a></p></td>
<td align="left"><p>このルーチンは、書式指定文字列と可変数のパラメーターを受け取りし、ログ記録が有効になっている場合は、I/O エラーのログ エントリとして記録するため、出力文字列の書式を設定します。</p>
<p>推奨されます、 <strong>RxLog</strong>このルーチンを直接呼び出す代わりにマクロを使用します。</p>
<p>このルーチンでは、Windows Server 2003、Windows XP、および Windows 2000 RDBSS のチェック ビルドで使用できるのみです。</p></td>
</tr>
</tbody>
</table>

 

次のマクロは、前の表に表示されているルーチンを呼び出す rxlog.h と rxprocs.h のヘッダー ファイルで定義されます。 これらのマクロは、通常これらのルーチンを直接呼び出す代わりに使用されます。

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
<td align="left"><p>チェック ビルドは、このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>_RxLog</strong> </a>ルーチン。</p>
<p>製品版ビルドでこのマクロは何もしません。</p>
<p>なお、引数を<strong>RxLog</strong>追加のログ記録をオフにするときに、null の呼び出しに変換を有効にするかっこのペアで囲む必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"> <strong>RxLogEventDirect</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>)</p></td>
<td align="left"><p>このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554515" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554515)"> <strong>RxLogEventDirect</strong> </a>ルーチン。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>, <em>_OriginatorId</em>, <em>_EventId</em>, <em>_Status</em>, <em>_Buffer</em>, <em>_Length</em>)</p></td>
<td align="left"><p>このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff554524" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554524)"> <strong>RxLogEventWithBufferDirect</strong> </a>ルーチン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogRetail</strong>(<em>Args</em>)</p></td>
<td align="left"><p>チェック ビルドは、このマクロを呼び出す、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557368" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557368)"> <strong>_RxLog</strong> </a>ルーチン。</p>
<p>製品版ビルドでこのマクロは何もしません。</p>
<p>なお、引数を<strong>RxLogRetail</strong>追加のログ記録をオフにするときに、null の呼び出しに変換を有効にするかっこのペアで囲む必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 




