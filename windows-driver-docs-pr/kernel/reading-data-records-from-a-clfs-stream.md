---
title: CLFS ストリームからのデータ レコードの読み取り
description: CLFS ストリームからのデータ レコードの読み取り
ms.assetid: 46e583c5-9f12-4f05-8f11-683ac428313a
keywords:
- WDK カーネル、データレコードの共通ログファイルシステム
- CLFS WDK カーネル、データレコード
- データレコード WDK CLFS
- データレコードの読み取り
- read forward WDK CLFS
- WDK CLFS の前方読み取り
- 後方 WDK CLFS の読み取り
- WDK CLFS の後方読み取り
- 前の LSNs WDK CLFS
- 元に戻す-next LSNs WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5209eee33b4946de530317857a010d8edce664d2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838474"
---
# <a name="reading-data-records-from-a-clfs-stream"></a>CLFS ストリームからのデータ レコードの読み取り


共通ログファイルシステム (CLFS) ストリームには、データレコードと再起動レコードの2種類のレコードがあります。 このトピックでは、ストリームから一連のデータレコードを読み取る方法について説明します。 再起動レコードを読み取る方法の詳細については、「 [CLFS ストリームからの再起動レコードの読み取り](reading-restart-records-from-a-clfs-stream.md)」を参照してください。

ストリームからの一連のデータレコードの読み取りには、いくつかのバリエーションがあります。 指定したレコードからストリームを読み取ることができます。または、リンクされたレコードのチェーンに沿って後方に読み取ることができます。

一連のデータレコードを読み取る際のすべてのバリエーションについて、次の手順を実行します。

1.  [**ClfsReadLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadlogrecord)を呼び出して、シーケンス内の読み取りコンテキストと最初のデータレコードを取得します。

2.  手順 1. で取得した読み取りコンテキストを[**ClfsReadNextLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadnextlogrecord)に渡して、シーケンス内の残りのデータレコードを取得します。

**注意**  読み取りコンテキストはスレッドセーフではありません。 クライアントは、読み取りコンテキストへのアクセスのシリアル化を行います。

 

次のサブトピックでは、さまざまな種類のレコードシーケンスとチェーンの読み取りの詳細について説明します。

### <a name="reading-forward-from-a-specified-data-record"></a>指定されたデータレコードからの読み取り

CLSF ストリームを (選択したデータレコードから) 読み取るには、そのモードが**Clfscontextforward**に設定された読み取りコンテキストを作成する必要があります。 読み取りコンテキストを作成し、(読み取り対象として選択したセット内の) 最初のレコードを読み取るには、次の表に示すように**ClfsReadLogRecord**を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvMarshalContext</em></p></td>
<td><p>マーシャリング領域へのポインターを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>読み取る最初のレコードの LSN を指定します。 これは、再起動レコードではなく、データレコードの LSN である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p><strong>Clfscontextforward</strong>の値を指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>レコードデータを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>レコードデータのサイズを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>レコードの種類を受信します。 この値は、レコードのさまざまな機能を示すフラグのセットです。 レコードはデータレコードであるため、受信する値には ClfsDataRecord フラグが設定され、ClfsRestartRecord フラグがクリアされている必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データレコードの undo (元に戻す) LSN を受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>データレコードの前の LSN を受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>不透明な読み取りコンテキストへのポインターを受け取ります。 後続のレコードを読み取るには、読み取りコンテキストを使用します。</p></td>
</tr>
</tbody>
</table>

 

読み取りコンテキストと最初のレコードを取得した後、 **ClfsReadNextLogRecord**を繰り返し呼び出して、ストリーム内の後続のレコードを取得できます。 ストリーム内にデータレコードがなくなった場合、 **ClfsReadNextLogRecord**は\_ファイルの\_終了\_ステータスを返します。 次の表は、パラメーターを設定および解釈する方法を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p><strong>ClfsReadLogRecord</strong>から受け取った読み取りコンテキストへのポインターを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>レコードデータを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbBuffer</em></p></td>
<td><p>レコードデータのサイズを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p><strong>ClfsDataRecord</strong>の値を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データレコードの [元に戻す] LSN フィールドを受信します。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>データレコードの前の LSN フィールドを受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>読み取られたデータレコードの LSN を受け取ります。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reading-a-chain-of-data-records-linked-by-the-previous-lsn"></a>前の LSN によってリンクされたデータレコードのチェーンを読み取る

データレコードを CLFS ストリームに書き込む場合、以前にストリームに書き込んだすべてのレコードの LSN にデータレコードの前の LSN を設定できます。 前の LSN を設定することによって、後で逆順に走査できる関連レコードのチェーンを作成できます。 たとえば、データベーストランザクションを実行しているときに、トランザクションによって行われた更新を説明するために、いくつかの CLFS ログレコードを書き込む必要があるとします。 トランザクションの更新を記述するログレコードを作成するたびに、レコードの前の LSN を、同じトランザクションによって行われた更新を示す前のログレコードの LSN に設定できます。

前の Lsn によってリンクされたデータレコードのチェーンを作成したとします。 レコードのチェーンを読み取るには、モードが**Clfscontextprevious**に設定された読み取りコンテキストを作成する必要があります。 読み取りコンテキストを作成し、チェーン内の最初のレコードを読み取るには、次の表に示すように**ClfsReadLogRecord**を呼び出します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvMarshalContext</em></p></td>
<td><p>マーシャリング領域へのポインターを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>チェーン内の最初のレコードの LSN を指定します。 これは、再起動レコードではなく、データレコードの LSN である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p><strong>Clfscontextprevious</strong>の値を指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>レコードデータを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>レコードデータのサイズを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>レコードの種類を受信します。 この値は、レコードのさまざまな機能を示すフラグのセットです。 レコードはデータレコードであるため、受信する値には ClfsDataRecord フラグが設定され、ClfsRestartRecord フラグがクリアされている必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データレコードの undo (元に戻す) LSN を受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>データレコードの前の LSN を受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>不透明な読み取りコンテキストへのポインターを受け取ります。 読み取りコンテキストを使用して、チェーン内の前のレコードを読み取ります。</p></td>
</tr>
</tbody>
</table>

 

読み取りコンテキストと最初のレコードを取得した後、 **ClfsReadNextLogRecord**を繰り返し呼び出すことで、チェーン内の残りのレコードを読み取ることができます。 次の表は、パラメーターを設定および解釈する方法を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p><strong>ClfsReadLogRecord</strong>から受け取った読み取りコンテキストへのポインターを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>レコードデータを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbBuffer</em></p></td>
<td><p>レコードデータのサイズを受け取ります。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p><strong>ClfsDataRecord</strong>の値を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データレコードの undo (元に戻す) LSN を受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>データレコードの前の LSN を受け取ります。 この値は、チェーンの読み取りを続けるためには必要ありません。そのため、無視してかまいません。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>読み取られたデータレコードの LSN を受け取ります。</p></td>
</tr>
</tbody>
</table>

 

**ClfsReadNextLogRecord**を繰り返し呼び出すと、呼び出しのシーケンスは次のいずれかの方法で終了します。

-   最終的には、前の LSN が CLFS に設定されているデータレコードを読み取り、LSN\_無効に\_ます。 次に**ClfsReadNextLogRecord**を呼び出したときに、\_ファイルの\_終了\_ステータスが返されます。

-   最終的には、ストリームのベース LSN とストリームの[*アーカイブテール*](clfs-terminology.md#kernel-clfs-term-archive-tail)の両方よりも前の lsn を持つデータレコードを読み取ります。 次に**ClfsReadNextLogRecord**を呼び出したときに、\_ログの\_開始\_の状態\_ログが返されます。

### <a name="reading-a-chain-of-data-records-linked-by-the-undo-next-lsn"></a>[元に戻す] LSN によってリンクされたデータレコードのチェーンを読み取る

データレコードを CLFS ストリームに書き込む場合は、データレコードの元に戻す LSN を、以前にストリームに書き込んだすべてのレコードの LSN に設定できます。 元に戻す LSN を設定することにより、逆の順序で走査できる関連レコードのチェーンを作成できます。 取り消し後のチェーンの作成と解釈の詳細については、「 [CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)」を参照してください。

元に戻す、次の Lsn によってリンクされるデータレコードのチェーンを作成したとします。 レコードのチェーンを読み取るには、 [**ClfsReadLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadlogrecord)を呼び出して、モードが**Clfscontextundonext**に設定された読み取りコンテキストを作成する必要があります。 その後、このプロセスは、前の Lsn でリンクされたチェーンの読み取りと同じです (このトピックで既に説明しています)。

### <a name="reading-a-chain-of-data-records-linked-by-the-user-lsn"></a>ユーザー LSN によってリンクされたデータレコードのチェーンを読み取る

前の Lsn によってリンクされたチェーンと、次の Lsn に加えて、レコードデータに埋め込む独自の Lsn によってリンクされたチェーンを作成できます。

レコードデータ自体に格納した Lsn によってリンクされたデータレコードのチェーンを作成したとします。 レコードのチェーンを読み取るには、そのモードが**Clfscontextprevious**または**Clfscontextundonext**に設定された読み取りコンテキストを作成する必要があります。 [**ClfsReadLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadlogrecord)を呼び出して、読み取りコンテキストを作成し、チェーン内の最後に記述されたレコードを取得します。 次に、 [**ClfsReadNextLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadnextlogrecord)を繰り返し呼び出して、チェーン内の前のレコードを取得します。 **ClfsReadNextLogRecord**を呼び出すたびに、 *plsnuser*パラメーターをチェーン内の前のレコードの LSN に設定します。 *Plsnuser*に指定した lsn は、現在のレコードの [前の lsn] フィールドまたは [元に戻す] lsn フィールドに格納されているすべての値をオーバーライドします。

**ClfsReadNextLogRecord**を呼び出してレコードチェーンを読み取る場合にのみ、ストリーム内で戻ることができます。 *Plsnuser*に指定する lsn は、チェーン内の現在のレコードの lsn より小さくなければなりません。

 

 




