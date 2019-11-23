---
title: CLFS ストリームへのデータ レコードの書き込み
description: CLFS ストリームへのデータ レコードの書き込み
ms.assetid: 22bd6d39-b777-4a62-85b1-3d03a7144f7a
keywords:
- WDK カーネル、データレコードの共通ログファイルシステム
- CLFS WDK カーネル、データレコード
- データレコード WDK CLFS
- 予約領域 WDK CLFS
- 固定エントリ (WDK CLFS)
- データレコードの書き込み
- バッファー WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1a30b9a762c0786afe862f2fe1cb108a4337da4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835574"
---
# <a name="writing-data-records-to-a-clfs-stream"></a>CLFS ストリームへのデータ レコードの書き込み





共通ログファイルシステム (CLFS) ストリームには、データレコードと再起動レコードの2種類のレコードがあります。 このトピックでは、データレコードをストリームに書き込む方法について説明します。 再起動レコードを書き込む方法については、「 [CLFS ストリームへの再起動レコードの書き込み](writing-restart-records-to-a-clfs-stream.md)」を参照してください。

CLFS ストリームにデータレコードを書き込むには、 [**ClfsCreateMarshallingArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatemarshallingarea)を呼び出してマーシャリング領域を作成する必要があります。 次に、マーシャリング領域 (揮発性メモリ内) にレコードを追加すると、CLFS は定期的にレコードを安定したストレージにフラッシュします。

ストリームへのデータレコードの書き込みには、いくつかのバリエーションがあります。 たとえば、領域を事前に予約してから複数のレコードを書き込むことができます。また、領域を予約せずにレコードを作成することもできます。 マーシャリング領域に書き込むレコードをすぐに安定したストレージにキューに入れるように要求できます。また、CLFS がそのポリシーに従ってレコードをキューに入れられるように要求することもできます。

データレコードの書き込みに関するすべてのバリエーションについて、次の手順を実行します。

1.  1つ以上の CLFS\_の配列を作成して[ **\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_write_entry)構造を書き込みます。 各書き込み構造体は、レコードデータを格納したバッファーを指します。

2.  [**ClfsReserveAndAppendLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlog)または[**ClfsReserveAndAppendLogAligned**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreserveandappendlogaligned)を呼び出します。

次のサブセクションの表は、ストリームへのレコードの書き込みに関するいくつかのバリエーションについて、 **ClfsReserveAndAppendLog**のパラメーターを設定する方法を示しています。

### <a name="writing-a-single-data-buffer-to-a-stream"></a>ストリームへの1つのデータバッファーの書き込み

マーシャリング領域に書き込むデータバッファーが1つあるとします。 CLFS ポリシーに従ってレコードを安定したストレージにフラッシュし、レコードをレコードのチェーンの一部にすることは避けたいと考えています。 次の表は、 **ClfsReserveAndAppendLog**を呼び出すときにパラメーターを設定する方法を示しています。

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
<td><p>マーシャリング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_write_entry" data-raw-source="[&lt;strong&gt;CLFS_WRITE_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_write_entry)"><strong>CLFS_WRITE_ENTRY</strong></a>構造体へのポインター。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_lsn" data-raw-source="[&lt;strong&gt;CLFS_LSN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cls_lsn)"><strong>CLFS_LSN</strong></a>構造体へのポインター。 (これは、書き込まれたレコードの LSN を受け取る出力パラメーターです)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reserving-space-for-a-set-of-clfs-log-records"></a>一連の CLFS ログレコードの領域を予約する

**ClfsReserveAndAppendLog**を使用すると、レコードを実際に書き込むことなく、一連のログレコードのマーシャリング領域に領域を予約できます。 次の表は、レコード領域を予約するパラメーターを設定する方法を示しています。

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
<td><p>マーシャリング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p><em>RgcbReservation</em>が指す配列内の要素の数。</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>LONGLONG 型の変数の配列へのポインター。 配列の各要素は、領域が予約されるレコードのサイズ (バイト単位) です。 これはレコードのデータ部分のサイズであることに注意してください。ヘッダーまたは埋め込みのサイズを含める必要はありません。</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p>NULL</p></td>
</tr>
</tbody>
</table>

 

**   マーシャリング**領域で領域を予約するもう1つの方法は、 [**ClfsAlignReservedLog**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsalignreservedlog)の後に[**clfsallocreのログ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsallocreservedlog)を呼び出すことです。

 

### <a name="writing-a-record-to-reserved-space"></a>予約領域へのレコードの書き込み

サイズ (バイト単位) が100、200、および300である3つのレコードに対して既に領域を予約しているとします。 マーシャリング領域には、予約済みのレコードカウント3と、600バイトのレコードデータを保持するのに十分な予約領域があり、レコードヘッダー、およびアラインメントに必要な埋め込みが格納されています。

ここで、これらのレコードの1つを、マーシャリング領域の予約済みの領域に書き込むとします。 使用可能な予約領域が減少し、予約済みレコード数が3から2に減少します。 次の表は、 **ClfsReserveAndAppendLog**を呼び出すときにパラメーターを設定する方法を示しています。

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
<td><p>マーシャリング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p><strong>CLFS_WRITE_ENTRY</strong>構造体の配列へのポインター。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p><em>RgWriteEntries</em>が指す配列内の要素の数。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>元に戻すチェーン内の前のレコードの CLFS_LSN_INVALID または LSN。 元に戻すチェーンの詳細については、「 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS Log Sequence Numbers</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>前の LSN チェーン内の前のログレコードの CLFS_LSN_INVALID または LSN。 前の LSN チェーンの詳細については、「 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS Log Sequence Numbers</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="even">
<td><p><em>fFlags</em></p></td>
<td><p>CLFS_FLAG_USE_RESERVATION</p></td>
</tr>
<tr class="odd">
<td><p><em>plsn</em></p></td>
<td><p><strong>CLFS_LSN</strong>構造体へのポインター。 (これは、書き込まれたレコードの LSN を受け取る出力パラメーターです)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="writing-records-with-aligned-entries"></a>固定されたエントリを使用したレコードの書き込み

3つの書き込みエントリを持つレコードを作成するとします。 書き込みエントリのサイズは300バイトと500バイトの間で異なりますが、各書き込みエントリは512バイト境界で開始される必要があります。 次の表は、 **ClfsReserveAndAppendLogAligned**関数のパラメーターを設定する方法を示しています。

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
<td><p>マーシャリング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>3つの CLFS_WRITE_ENTRY 構造体の配列へのポインター。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>3</p></td>
</tr>
<tr class="even">
<td><p><em>cbEntryAlignment</em></p></td>
<td><p>512</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>元に戻すチェーン内の前のレコードの CLFS_LSN_INVALID または LSN。 元に戻すチェーンの詳細については、「 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS Log Sequence Numbers</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>前の LSN チェーン内の前のログレコードの CLFS_LSN_INVALID または LSN。 前の LSN チェーンの詳細については、「 <a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS Log Sequence Numbers</a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em>cReserveRecords</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>rgcbReservation</em></p></td>
<td><p>NULL</p></td>
</tr>
<tr class="odd">
<td><p><em>fFlags</em></p></td>
<td><p>フラッシュと予約の設定を指定する0個以上のフラグの組み合わせ。</p></td>
</tr>
<tr class="even">
<td><p><em>plsn</em></p></td>
<td><p>CLFS_LSN 構造体へのポインター。 (これは、書き込まれたレコードの LSN を受け取る出力パラメーターです)。</p></td>
</tr>
</tbody>
</table>

 

上の表は、レコード領域の予約と CLFS ストリームへのレコードの書き込みに関する多くのバリエーションを示しています。 他のバリエーションを考えながら、次の点に注意してください。 **ClfsReserveAndAppendLog** (または**ClfsReserveAndAppendLogAligned**) によって実行されるアクションはアトミックです。 たとえば、レコードの領域を予約し、そのレコードをストリームに書き込む**ClfsReserveAndAppendLog**の1回の呼び出しを行うことができます。 アクション (予約、書き込み) のペアは、全体として成功するか、全体が失敗します。

 

 




