---
title: CLFS ストリームからのデータ レコードの読み取り
description: CLFS ストリームからのデータ レコードの読み取り
ms.assetid: 46e583c5-9f12-4f05-8f11-683ac428313a
keywords:
- 一般的なログ ファイル システムの WDK カーネルでは、データ レコード
- CLFS WDK カーネルでは、データ レコード
- データ レコードを WDK CLFS
- データ レコードの読み取り
- 前方の WDK CLFS を読み取る
- WDK CLFS を読み取り中を転送します。
- 旧バージョンとの WDK CLFS を読み取る
- 後方 WDK CLFS の読み取り
- 前の Lsn WDK CLFS
- 次への元に戻す Lsn WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02a83d13ff1d5dfac77e0dd5e9430f0510124a1c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378753"
---
# <a name="reading-data-records-from-a-clfs-stream"></a>CLFS ストリームからのデータ レコードの読み取り


Common Log File System (CLFS) ストリーム内のレコードの 2 種類があります。 データがレコードとレコードを再起動します。 このトピックでは、データ レコードのシーケンスをストリームから読み取る方法について説明します。 再起動のレコードを読み取る方法については、次を参照してください。 [CLFS Stream から読み取りを再開レコード](reading-restart-records-from-a-clfs-stream.md)します。

ストリームからデータ レコードのシーケンスの読み取りでいくつかのバリエーションがあります。 転送、指定されたレコードからのストリームに読み取ることができますか、後方リンクされたレコードのチェーンに読み取ることができます。

すべてのバリエーションでデータ レコードのシーケンスを読み取り、次の手順を完了します。

1.  呼び出す[ **ClfsReadLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadlogrecord)読み取りコンテキストと、シーケンス内の最初のデータ レコードを取得します。

2.  手順 1 で取得した読み取りコンテキストを渡す[ **ClfsReadNextLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadnextlogrecord)シーケンス内の残りのデータ レコードを取得するために繰り返し。

**注意**  読み取りコンテキストはスレッド セーフではありません。 クライアントは、コンテキストの読み取りアクセス許可をシリアル化する責任を負います。

 

次のサブトピックでは、レコード シーケンスとチェーンのさまざまな種類の読み取りの詳細について説明します。

### <a name="reading-forward-from-a-specified-data-record"></a>転送を指定したデータ レコードから読み取る

設定を読み取るように転送 (任意のデータ レコードから始まります)、CLSF ストリームのモードになっている読み取りコンテキストを作成する必要があります**ClfsContextForward**します。 読み取りコンテキストを作成し、(読み取り、選択したセット) 内の最初のレコードを読み取り、 **ClfsReadLogRecord**次の表に示すようにします。

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
<td><p>マーシャ リング領域へのポインターを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>読み取る最初のレコードの LSN を指定します。 これには、再起動レコードではなく、データ レコードの LSN があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p>値の指定<strong>ClfsContextForward</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>レコード データを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>レコード データのサイズが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>レコードの種類が表示されます。 この値は、一連のレコードのさまざまな機能を示すフラグです。 レコードは、受信した値が ClfsDataRecord フラグの設定を利用する必要がありますあり ClfsRestartRecord フラグのクリアのデータ レコードです。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データ レコードの元に戻す次の LSN が表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>前のデータ レコードの LSN が表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>非透過の読み込みコンテキストへのポインターが表示されます。 読み取りコンテキストを使用して、その後のレコードを読み取ります。</p></td>
</tr>
</tbody>
</table>

 

読み取りコンテキストと最初のレコードを取得した後は、呼び出すことによって、ストリーム内の後続のレコードを取得できます**ClfsReadNextLogRecord**繰り返し。 ストリームのデータ レコードがある場合に**ClfsReadNextLogRecord**ステータスを返します\_エンド\_の\_ファイル。 次の表では、設定し、パラメーターの解釈する方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p>受信した読み取りコンテキストへのポインターを指定<strong>ClfsReadLogRecord</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>レコード データを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>書き込ま</em></p></td>
<td><p>レコード データのサイズが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>値を与える<strong>ClfsDataRecord</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データ レコードの元に戻す次の LSN フィールドが表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>データのレコードの LSN 前のフィールドが表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>読み取られたデータ レコードの LSN が表示されます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reading-a-chain-of-data-records-linked-by-the-previous-lsn"></a>前の LSN によってリンクされているデータ レコードのチェーンの読み取り

CLFS ストリームからデータ レコードを書き込む場合は、ストリームに以前作成した任意のレコードの LSN を前のデータ レコードの LSN を設定できます。 前の LSN を設定するには、逆の順序で走査することが後で関連レコードのチェーンを作成できます。 たとえば、データベースのトランザクションを実行して、トランザクションによって加えられた更新プログラムを記述するいくつかの CLFS ログ レコードを書き込む必要があります。 トランザクションの更新プログラム、について説明するログ レコードを作成するたびに同じトランザクションによって加えられた更新プログラムを記述する前のログ レコードの LSN を前のレコードの LSN を設定できます。

前の Lsn によってリンクされているデータ レコードのチェーンを記述したとします。 レコードのチェーンを読み取り、モードを設定読み取りのコンテキストを作成する必要があります**ClfsContextPrevious**します。 読み取りコンテキストを作成し、チェーン内の最初のレコードを読み取り、 **ClfsReadLogRecord**次の表に示すようにします。

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
<td><p>マーシャ リング領域へのポインターを指定します。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnFirst</em></p></td>
<td><p>チェーンの最初のレコードの LSN を指定します。 これには、再起動レコードではなく、データ レコードの LSN があります。</p></td>
</tr>
<tr class="odd">
<td><p><em>peContextMode</em></p></td>
<td><p>値を与える<strong>ClfsContextPrevious</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvReadBuffer</em></p></td>
<td><p>レコード データを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>pcbReadBuffer</em></p></td>
<td><p>レコード データのサイズが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>レコードの種類が表示されます。 この値は、一連のレコードのさまざまな機能を示すフラグです。 レコードは、受信した値が ClfsDataRecord フラグの設定を利用する必要がありますあり ClfsRestartRecord フラグのクリアのデータ レコードです。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データ レコードの元に戻す次の LSN が表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>前のデータ レコードの LSN が表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="odd">
<td><p><em>ppvReadContext</em></p></td>
<td><p>非透過の読み込みコンテキストへのポインターが表示されます。 読み取りコンテキストを使用して、チェーン内の前のレコードを読み取ります。</p></td>
</tr>
</tbody>
</table>

 

読み取りコンテキストと最初のレコードを作成したら、呼び出すことによって、チェーン内の残りのレコードを読み取ることができます**ClfsReadNextLogRecord**繰り返し。 次の表では、設定し、パラメーターの解釈する方法を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター名</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>pvReadContext</em></p></td>
<td><p>受信した読み取りコンテキストへのポインターを指定<strong>ClfsReadLogRecord</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><em>ppvBuffer</em></p></td>
<td><p>レコード データを受信します。</p></td>
</tr>
<tr class="odd">
<td><p><em>書き込ま</em></p></td>
<td><p>レコード データのサイズが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>peRecordType</em></p></td>
<td><p>値を与える<strong>ClfsDataRecord</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>データ レコードの元に戻す次の LSN が表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>前のデータ レコードの LSN が表示されます。 これを無視することができますので、チェーンの読み取りを続行するには、この値は不要です。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnRecord</em></p></td>
<td><p>読み取られたデータ レコードの LSN が表示されます。</p></td>
</tr>
</tbody>
</table>

 

繰り返しの呼び出しを行うと**ClfsReadNextLogRecord**呼び出しのシーケンスは、次の方法のいずれかで終了します。

-   CLFS を設定、以前の LSN を含むデータ レコードを読み取りが最終的に\_LSN\_が無効です。 [次へ] を呼び出すまで**ClfsReadNextLogRecord**、状態が返されます\_エンド\_の\_ファイル。

-   前の LSN は、ストリームより小さい両方のベース LSN を持つデータ レコードを読み取りが最終的に、 [*アーカイブ末尾*](clfs-terminology.md#kernel-clfs-term-archive-tail)のストリーム。 [次へ] を呼び出すまで**ClfsReadNextLogRecord**、状態が返されます\_ログ\_開始\_の\_ログ。

### <a name="reading-a-chain-of-data-records-linked-by-the-undo-next-lsn"></a>元に戻す次の LSN によってリンクされているデータ レコードのチェーンの読み取り

CLFS ストリームからデータ レコードを書き込む場合は、ストリームに以前作成した任意のレコードの LSN をデータ レコードの元に戻す次の LSN を設定できます。 元に戻す次の LSN を設定するには、逆の順序で走査できる関連するレコードのチェーンを作成できます。 作成して、元に戻す次チェーンの解釈の詳細については、次を参照してください。 [CLFS ログ シーケンス番号](clfs-log-sequence-numbers.md)します。

元に戻す次の Lsn によってリンクされているデータ レコードのチェーンを記述したとします。 レコードのチェーンを読み取りを呼び出す必要がある[ **ClfsReadLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadlogrecord)そのモードになっている読み取りコンテキストを作成する設定**ClfsContextUndoNext**します。 その後、プロセスは、(このトピックで既に説明した) 前回の Lsn によってリンクされているチェーンの読み取りと同じです。

### <a name="reading-a-chain-of-data-records-linked-by-the-user-lsn"></a>ユーザーの LSN によってリンクされているデータ レコードのチェーンの読み取り

だけでなく、以前の Lsn と元に戻す次の Lsn によってリンクされているチェーン、レコードのデータに埋め込むことが、独自の Lsn によってリンクされているチェーンを作成できます。

レコード データ自体に保管されている Lsn によってリンクされているデータ レコードのチェーンを記述したとします。 レコードのチェーンを読み取り、そのモードのいずれかに設定された読み取りのコンテキストを作成する必要が**ClfsContextPrevious**または**ClfsContextUndoNext**します。 読み取りのコンテキストを作成し、呼び出すことによって、チェーンの直前に書き込まれたレコードを取得[ **ClfsReadLogRecord**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadlogrecord)します。 呼び出して[ **ClfsReadNextLogRecord** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadnextlogrecord)チェーン内の前のレコードを取得するために繰り返し。 呼び出すたびに**ClfsReadNextLogRecord**、設定、 *plsnUser*パラメーター、チェーンの前のレコードの lsn。 指定した LSN *plsnUser*現在のレコードの LSN 前または次への元に戻す LSN フィールドに格納されている値を上書きします。

ことができますのみ後方に移動、ストリームを呼び出すときに注意してください**ClfsReadNextLogRecord**レコードのチェーンを読み込むことです。 指定した LSN *plsnUser*チェーン内の現在のレコードの LSN よりも小さい必要があります。

 

 




