---
title: CLFS Stream へのデータ レコードの書き込み
description: CLFS Stream へのデータ レコードの書き込み
ms.assetid: 22bd6d39-b777-4a62-85b1-3d03a7144f7a
keywords:
- 一般的なログ ファイル システムの WDK カーネルでは、データ レコード
- CLFS WDK カーネルでは、データ レコード
- データ レコードを WDK CLFS
- 予約領域 WDK CLFS
- アラインされたエントリ WDK CLFS
- データ レコードの書き込み
- WDK CLFS をバッファー処理します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f817b8406a1d5ad041ba418004b09e1ed9f13e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539315"
---
# <a name="writing-data-records-to-a-clfs-stream"></a>CLFS Stream へのデータ レコードの書き込み





Common Log File System (CLFS) ストリーム内のレコードの 2 種類があります。 データがレコードとレコードを再起動します。 このトピックでは、データ レコードをストリームに書き込む方法について説明します。 再起動のレコードを作成する方法については、[CLFS Stream にの再開レコードの書き込み](writing-restart-records-to-a-clfs-stream.md)を参照してください。

データ レコードを作成するには、CLFS ストリームに、前に呼び出すことによって、マーシャ リング領域を作成する必要があります[ **ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)します。 (これは揮発性メモリ内に) マーシャ リング領域にレコードを追加でき、CLFS は安定ストレージにレコードを定期的にフラッシュします。

ストリームへのデータ レコードの書き込みに関するいくつかのバリエーションがあります。 たとえば、事前に領域を予約して、複数のレコードを作成し、または領域を予約しないでのレコードを書き込むことができます。 マーシャ リング領域に記述するレコードのすぐにキューに安定したストレージは、登録を要求することができます、またはキューにそのポリシーに従ってレコード CLFS をさせることができます。

すべてのバリエーション データ レコードの作成では、次の手順を完了します。

1.  1 つまたは複数の配列を作成する[ **CLFS\_書き込み\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff541891)構造体。 各書き込みエントリの構造は、レコードのデータを入力したらバッファーを指します。

2.  呼び出す[ **ClfsReserveAndAppendLog** ](https://msdn.microsoft.com/library/windows/hardware/ff541723)または[ **ClfsReserveAndAppendLogAligned**](https://msdn.microsoft.com/library/windows/hardware/ff541726)します。

次のサブセクションでは、テーブルのパラメーターを設定する方法を表示する**ClfsReserveAndAppendLog**のストリームへのレコードの書き込みに関するいくつかのバリエーション。

### <a name="writing-a-single-data-buffer-to-a-stream"></a>ストリームに 1 つのデータ バッファーを書き込む

マーシャ リング領域への書き込みにする 1 つのデータ バッファーがあるとします。 CLFS ポリシーに基づく安定ストレージにフラッシュするレコードを使用して、レコードの任意のチェーンの一部であるレコードしたくないです。 次の表は、呼び出すときに、パラメーターを設定する方法を示します**ClfsReserveAndAppendLog**します。

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
<td><p>マーシャ リング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff541891" data-raw-source="[&lt;strong&gt;CLFS_WRITE_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541891)"> <strong>CLFS_WRITE_ENTRY</strong> </a>構造体。</p></td>
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
<td><p>ポインターを<a href="https://msdn.microsoft.com/library/windows/hardware/ff541824" data-raw-source="[&lt;strong&gt;CLFS_LSN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541824)"> <strong>CLFS_LSN</strong> </a>構造体。 (これは、書き込まれるレコードの LSN を受信する出力パラメーターです)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="reserving-space-for-a-set-of-clfs-log-records"></a>CLFS ログ レコードのセットの領域を予約

使用することができます**ClfsReserveAndAppendLog**を実際には、レコードのいずれかを記述することがなく一連のログ レコードのマーシャ リング領域内の領域を予約します。 次の表では、レコードの領域を予約するパラメーターを設定する方法を示します。

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
<td><p>マーシャ リング領域へのポインター。</p></td>
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
<td><p>配列内の要素の数が指す<em>rgcbReservation</em>します。</p></td>
</tr>
<tr class="odd">
<td><p><em>rgcbReservation</em></p></td>
<td><p>LONGLONG に型指定された変数の配列へのポインター。 配列内の各要素は、サイズ、領域を予約するレコードのバイト単位です。 このレコードのデータ部分のサイズは、このことに注意してください。ヘッダーまたは余白のサイズを含める必要はありません。</p></td>
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

 

**注**  マーシャ リング領域内の領域を予約する別の方法を呼び出すことです[ **ClfsAlignReservedLog** ](https://msdn.microsoft.com/library/windows/hardware/ff540779)続けて[ **ClfsAllocReservedLog。**](https://msdn.microsoft.com/library/windows/hardware/ff540782).

 

### <a name="writing-a-record-to-reserved-space"></a>予約された領域に、レコードの書き込み

(バイト単位) のサイズは 200、および 300 の 3 つのレコードの領域が既に予約されているとします。 マーシャ リングの領域のデータを記録、レコード ヘッダー、および配置に必要なすべての埋め込みの 600 バイトを保持するために 3 と十分な予約済みの領域の予約レコード数があります。

今すぐを記述したいとしますうちの 1 つをマーシャ リング領域で予約した領域に記録します。 使用可能な予約された領域は削減は、および予約レコード数は 2、3 から差し引かれるになります。 次の表は、呼び出すときに、パラメーターを設定する方法を示します**ClfsReserveAndAppendLog**します。

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
<td><p>マーシャ リング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>配列へのポインター <strong>CLFS_WRITE_ENTRY</strong>構造体。</p></td>
</tr>
<tr class="odd">
<td><p><em>cWriteEntries</em></p></td>
<td><p>配列内の要素の数が指す<em>rgWriteEntries</em>します。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnUndoNext</em></p></td>
<td><p>CLFS_LSN_INVALID または元に戻すチェーンの前のレコードの LSN。 元に戻すチェーンの詳細については、<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS ログ シーケンス番号</a>を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID または以前 LSN チェーンの前のログ レコードの LSN。 以前 LSN チェーンの詳細については、<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS ログ シーケンス番号</a>を参照してください。</p></td>
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
<td><p>ポインターを<strong>CLFS_LSN</strong>構造体。 (これは、書き込まれるレコードの LSN を受信する出力パラメーターです)。</p></td>
</tr>
</tbody>
</table>

 

### <a name="writing-records-with-aligned-entries"></a>配置済みのエントリを持つレコードの書き込み

3 つの書き込みエントリを持つレコードを作成するとします。 サイズは 300 および 500 件のバイト範囲書き込みエントリが異なりますが、書き込みの各エントリが 512 バイト境界で開始することが必要です。 次の表のパラメーターを設定する方法を示します、 **ClfsReserveAndAppendLogAligned**関数。

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
<td><p>マーシャ リング領域へのポインター。</p></td>
</tr>
<tr class="even">
<td><p><em>rgWriteEntries</em></p></td>
<td><p>次の 3 つの CLFS_WRITE_ENTRY 構造体の配列へのポインター。</p></td>
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
<td><p>CLFS_LSN_INVALID または元に戻すチェーンの前のレコードの LSN。 元に戻すチェーンの詳細については、<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS ログ シーケンス番号</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><p><em>plsnPrevious</em></p></td>
<td><p>CLFS_LSN_INVALID または以前 LSN チェーンの前のログ レコードの LSN。 以前 LSN チェーンの詳細については、<a href="clfs-log-sequence-numbers.md" data-raw-source="[CLFS Log Sequence Numbers](clfs-log-sequence-numbers.md)">CLFS ログ シーケンス番号</a>を参照してください。</p></td>
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
<td><p>フラッシュと予約の設定を指定するフラグの 0 個またはいくつかの組み合わせ。</p></td>
</tr>
<tr class="even">
<td><p><em>plsn</em></p></td>
<td><p>CLFS_LSN 構造体へのポインター。 (これは、書き込まれるレコードの LSN を受信する出力パラメーターです)。</p></td>
</tr>
</tbody>
</table>

 

上記の表では、レコードの領域を予約すると、レコードを CLFS ストリームに書き込むだけ多くのバリエーションのいくつかを示します。 他のバリエーションの思いは、次の点に留意してください。によって実行されたアクション**ClfsReserveAndAppendLog** (または**ClfsReserveAndAppendLogAligned**) はアトミックです。 たとえば、1 回の呼び出しを行うことができます**ClfsReserveAndAppendLog**レコードの領域を予約され、レコードをストリームに書き込むです。 (予約、書き込み) 操作のペアが全体として成功または全体が失敗します。

 

 




