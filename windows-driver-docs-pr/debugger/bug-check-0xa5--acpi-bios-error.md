---
title: バグチェック 0xA5 ACPI_BIOS_ERROR
description: ACPI_BIOS_ERROR のバグチェックには、コンピューターの ACPI BIOS が ACPI 仕様に完全に準拠していないことを示す値0x000000A5 があります。
ms.assetid: f0366a3c-a2c4-4fc8-a722-52fdda59eb2b
keywords:
- バグチェック 0xA5 ACPI_BIOS_ERROR
- ACPI_BIOS_ERROR
ms.date: 09/12/2019
topic_type:
- apiref
api_name:
- ACPI_BIOS_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4975f922f3c347f58a596010a2b5fd91b3649401
ms.sourcegitcommit: f91a0fd22f46be44839d2a22a21f59fad900ce90
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71020989"
---
# <a name="bug-check-0xa5-acpi_bios_error"></a>バグ チェック 0xA5:ACPI\_BIOS\_エラー

ACPI\_BIOS\_エラーのバグチェックには、0x000000A5 の値が含まれています。 このバグチェックは、コンピューターの Advanced Configuration and Power Interface (ACPI) BIOS が ACPI 仕様に完全に準拠していないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="acpi_bios_error-parameters"></a>ACPI\_BIOS\_エラーパラメーター

パラメーター1は非互換性の種類を示します。 他のパラメーターの意味は、パラメーター1の値によって異なります。

BIOS の非互換性がプラグアンドプレイ (PnP) または電源管理に関連している場合は、次のパラメーターが使用されます。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ACPI の<strong>Deviceextension</strong></p></td>
<td align="left"><p>ACPI の<strong>Resourcelist</strong></p></td>
<td align="left"><p><strong>0</strong>リソースリストが見つかりません</p>
<p><strong>1:</strong>一覧に IRQ リソースが見つかりません</p></td>
<td align="left"><p>Acpi は、ACPI が開始されたときに、システム制御割り込み (SCI) によって渡されたリソースを見つけることができません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(このページの後の表を参照)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>実行されていた ACPI オブジェクト</p></td>
<td align="left"><p>インタープリターからの戻り値</p></td>
<td align="left"><p>コントロールメソッドの名前 (ULONG 形式)</p></td>
<td align="left"><p>Acpi は、ACPI 名前空間を表すデバイス拡張を作成しているときに、制御メソッドを実行しようとしましたが、この制御方法は失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>_PRW が属している ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p>返される<strong>データ型</strong>(「amli」を参照)</p></td>
<td align="left"><p>ACPI は _PRW を評価し、パッケージ要素として整数を検索することを想定しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>_PRW が属している ACPI 拡張機能</p></td>
<td align="left"><p>_PRW</p></td>
<td align="left"><p>_PRW 内の要素の数</p></td>
<td align="left"><p>ACPI は _PRW を評価し、返されたパッケージには少なくとも2つの要素を含めることができませんでした。 ACPI 仕様では、2つの要素が常に _PRW に存在している必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>に属している ACPI 拡張機能</p></td>
<td align="left"><p>Prx へのポインター</p></td>
<td align="left"><p>検索するオブジェクトの名前へのポインター</p></td>
<td align="left"><p>ACPI は名前付きオブジェクトを見つけようとしましたが、オブジェクトが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p>返される<strong>データ型</strong>(「amli」を参照)</p></td>
<td align="left"><p>ACPI はメソッドを評価し、返されたバッファーを受け取ることを想定していました。 ただし、メソッドによって他のデータ型が返されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p>返される<strong>データ型</strong>(「amli」を参照)</p></td>
<td align="left"><p>ACPI はメソッドを評価し、返された整数を受け取ることを想定していました。 ただし、メソッドによって他のデータ型が返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p>返される<strong>データ型</strong>(「amli」を参照)</p></td>
<td align="left"><p>ACPI がメソッドを評価し、返されたパッケージを受け取ることを想定しています。 ただし、メソッドによって他のデータ型が返されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p>返される<strong>データ型</strong>(「amli」を参照)</p></td>
<td align="left"><p>ACPI はメソッドを評価し、返された文字列を受け取ることを想定していました。 ただし、メソッドによって他のデータ型が返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>_EJD が属している ACPI 拡張機能</p></td>
<td align="left"><p>インタープリターが返す状態</p></td>
<td align="left"><p>ACPI が検索しようとしているオブジェクトの名前</p></td>
<td align="left"><p>ACPI は、_EJD 文字列で参照されているオブジェクトを見つけることができません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ACPI がドッキングデバイスを検出した ACPI 拡張機能</p></td>
<td align="left"><p>_EJD メソッドへのポインター</p></td>
<td align="left"><p><strong>0</strong>BIOS はシステムの dockage を要求しません</p>
<p><strong>1:</strong>ドッキングデバイスのデバイス拡張機能が重複しています</p></td>
<td align="left"><p>ACPI では、dock サポートに関する情報が不足しているか、不十分です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ACPI がオブジェクトを必要とする ACPI 拡張機能</p></td>
<td align="left"><p>ACPI によって検索されたメソッドの (ULONG) 名</p></td>
<td align="left"><p><strong>0</strong>基本ケース</p>
<p><strong>1:</strong>Conflict</p></td>
<td align="left"><p>ACPI は名前空間に必要なメソッドまたはオブジェクトを見つけることができませんでした。このバグチェックコードは、HID または ADR が存在しない場合に使用されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>ACPI がオブジェクトを必要とする NS <strong>Powerresource</strong></p></td>
<td align="left"><p>ACPI によって検索されたメソッドの (ULONG) 名</p></td>
<td align="left"><p>0基本ケース</p></td>
<td align="left"><p>ACPI は、電源リソース (または "デバイス" 以外のエンティティ) の名前空間に必要なメソッドまたはオブジェクトを見つけることができませんでした。 このバグチェックコードは、電源リソースに対して存在するものがない場合に使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>ACPI が解析した現在のバッファー</p></td>
<td align="left"><p>バッファーのタグ</p></td>
<td align="left"><p>バッファーの指定された長さ</p></td>
<td align="left"><p>ACPI がリソース記述子を解析できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(このページの後の表を参照)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(このページの後の表を参照)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ACPI が解析した現在のバッファー</p></td>
<td align="left"><p>バッファーのタグ</p></td>
<td align="left"><p>バッファーの ULONGLONG の長さを格納する変数へのポインター</p></td>
<td align="left"><p>ACPI がリソース記述子を解析できませんでした。 長さが MAXULONG を超えています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ACPI 機械言語 (AML) のコンテキスト</p></td>
<td align="left"><p><strong>1:</strong>テーブルを読み込めませんでした</p>
<p><strong>2:</strong>パラメーターパス文字列オブジェクトが見つかりませんでした</p>
<p><strong>3時</strong>パラメーターデータを ParameterPath 文字列オブジェクトに挿入できませんでした</p>
<p><strong>4時</strong>システムメモリが不足しています</p></td>
<td align="left"><p>NT 状態コード</p></td>
<td align="left"><p>ACPI で、テーブルを読み込もうとしたときに致命的なエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>親 NSOBJ へのポインター</p></td>
<td align="left"><p>無効な子 ACPI 名前空間オブジェクトへのポインター</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>XSDT の処理中に、ACPI で致命的なエラーが発生しました。 オブジェクトが、子を持つことができない親の子として宣言されました。</p></td>
</tr>
</tbody>
</table>

 

割り込みルーティングの失敗または非互換性が発生した場合は、次のパラメーターが使用されます。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p><strong>InterruptModel</strong>以外</p></td>
<td align="left"><p>インタープリターからの戻り値</p></td>
<td align="left"><p>PIC コントロールメソッドへのポインター</p></td>
<td align="left"><p>ACPI は PIC 制御メソッドを評価しようとしましたが、失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10001</p></td>
<td align="left"><p>デバイスオブジェクトへのポインター</p></td>
<td align="left"><p>デバイスオブジェクトの親へのポインター</p></td>
<td align="left"><p>PRT オブジェクトへのポインター</p>
<p>(次のコメントセクションを参照してください)。</p></td>
<td align="left"><p>ACPI は割り込みルーティングを実行しようとしましたが、失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10002</p></td>
<td align="left"><p>デバイスオブジェクトへのポインター</p></td>
<td align="left"><p>ACPI が検索する文字列名を指すポインターですが、見つかりませんでした。</p></td>
<td align="left"><p>PRT オブジェクトへのポインター</p>
<p>(次のコメントセクションを参照してください)。</p></td>
<td align="left"><p>ACPI は、PRT で参照されているリンクノードを見つけることができませんでした。 (_s)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10003</p></td>
<td align="left"><p>デバイスオブジェクトへのポインター</p></td>
<td align="left"><p>デバイス ID または関数番号。</p>
<p>この DWORD は、次のようにエンコードされます。ビット5:0 は PCI デバイス番号、bits 8:6 は PCI 関数の番号です。</p></td>
<td align="left"><p>PRT オブジェクトへのポインター</p>
<p>(次のコメントセクションを参照してください)。</p></td>
<td align="left"><p>ACPI は、デバイスのパッケージでマッピングを見つけることができませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10005</p></td>
<td align="left"><p>PRT オブジェクトへのポインター</p>
<p>(次のコメントセクションを参照してください)。</p></td>
<td align="left"><p>現在の要素へのポインター。</p>
<p>(このポインターは、PRT へのインデックスです)。</p></td>
<td align="left"><p>デバイス ID または関数番号。</p>
<p>この DWORD は、次のようにエンコードされます。ビット15:0 は PCI 関数番号、bits 31:16 は PCI デバイス番号です。</p></td>
<td align="left"><p>ACPI が、関数 ID が F のすべてではないというエントリを PRT に検出しました。</p>
<p>(PRT エントリの汎用形式では、デバイス番号が指定されていますが、関数番号が指定されていません)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10006</p></td>
<td align="left"><p>リンクノードへのポインター。</p>
<p>(このデバイスには、メソッドがありません)。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI がリンクノードを検出しましたが、ノードを無効にすることはできません。</p>
<p>(Reprogramming を許可するには、リンクノードを無効にする必要があります。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10007</p></td>
<td align="left"><p>見つからなかったベクター</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>I/O APIC エントリの MAPIC テーブルに記述されていないベクターへの参照が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10008</p></td>
<td align="left"><p>無効な割り込みレベルです。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI SCI 割り込みレベルが無効です。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10009</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>修正された ACPI 説明テーブル (FADT) が見つかりませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000A</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ルートシステム記述ポインター (RSDP) または拡張システム記述テーブル (XSDT) が見つかりませんでした</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000B</p></td>
<td align="left"><p>ACPI テーブル署名</p></td>
<td align="left"><p>ACPI テーブルへのポインター</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI テーブルの長さとテーブルのリビジョンが一致していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000C</p></td>
<td align="left"><p>リビジョン ID</p></td>
<td align="left"><p>関数のインデックス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>割り込みの DSM メソッドが間違った形式のデータを返しました。 (_c)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000D</p></td>
<td align="left"><p>デバイスの ACPI 拡張機能</p></td>
<td align="left"><p>値 0: wake 対応の割り込みがなく、少なくとも1つの GPIO 割り込み値1が指定されている _PRW。ウェイク対応の割り込みがあるため、_PRW は、0xffffffff の GpeInfo 値を指定する必要があります。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>デバイスで、GPE と GPIO の両方の割り込みが使用されていますが、これはサポートされていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000E</p></td>
<td align="left"><p></p>検証関数によって返される状態。</td>
<td align="left"><p> ACPI 名前空間パス UNICODE_STRING へのポインター。</p></td>
<td align="left"><p>SDEV と比較した場合のリソースリストへのポインター。</p></td>
<td align="left"><p>セキュリティで保護されたデバイスの SDEV リソースが、対応する CRS または _PRS entry と一致しません。</p></td>
</tr>
</tbody>
</table>

その他の障害または非互換性が発生した場合は、次のパラメーターが使用されます。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x20000</p></td>
<td align="left"><p>固定テーブルの i/o ポート</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>Fixed ACPI Description テーブルの PM_TMR_BLK エントリは、動作する ACPI タイマーブロックを指していません。</p></td>
</tr>
</tbody>
</table>

次の表では、次のパラメーターが使用される場合のメモリ使用量の問題について説明します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>メモリ領域の物理アドレスの上位部分。</p></td>
<td align="left"><p>メモリ領域の物理アドレスの下位部分。</p></td>
<td align="left"><p>割り当てられるメモリの長さ。</p></td>
<td align="left"><p>ACPI でメモリ操作領域を処理中に致命的なエラーが発生しました。 メモリ操作領域は、OS の使用に割り当てられているメモリをマップしようとしました。</p></td>
</tr>
</tbody>
</table>


パラメーター1が**0x02**の場合、ACPI BIOS は PCI ルートバスのリソースリストを処理できませんでした。 この場合、パラメーター3は正確な問題を指定し、残りのパラメーターには次の定義が含まれます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PCI バス用の ACPI 拡張機能</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>QUERY_RESOURCES IRP へのポインター</p></td>
<td align="left"><p>ACPI は、BIOS のリソースの一覧を適切な形式に変換できません。 これは、BIOS の list encoding プロシージャのエラーを表している場合があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCI バス用の ACPI 拡張機能</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>QUERY_RESOURCE_REQUIREMENTS IRP へのポインター</p></td>
<td align="left"><p>ACPI は、BIOS のリソースの一覧を適切な形式に変換できません。 これは、BIOS の list encoding プロシージャのエラーを表している場合があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCI バス用の ACPI 拡張機能</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI が空のリソースリストを検出しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCI バス用の ACPI 拡張機能</p></td>
<td align="left"><p>0x3</p></td>
<td align="left"><p>PNP CRS 記述子へのポインター</p></td>
<td align="left"><p>ACPI は、CRS で現在のバス番号を見つけることができませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCI バス用の ACPI 拡張機能</p></td>
<td align="left"><p>PCI のリソースリストへのポインター</p></td>
<td align="left"><p>E820 memory テーブルへのポインター</p></td>
<td align="left"><p>PCI 要求がデコードされるリソースの一覧が、E820 BIOS インターフェイスによって報告されるメモリ領域の一覧と重複しています。 (この種類の競合は許可されません)。</p></td>
</tr>
</tbody>
</table>

 

パラメーター1が**0x10**の場合、ACPI BIOS は、システムとデバイスの間のマッピングを正しく判断できませんでした。 この場合、パラメーター3は正確な問題を指定し、残りのパラメーターには次の定義が含まれます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>マッピングが必要な ACPI 拡張機能</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>DEVICE_POWER_STATE ("x + 1")</p></td>
<td align="left"><p>Prx はサポートされていない状態にマップされました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>マッピングが必要な ACPI 拡張機能</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>マップできない SYSTEM_POWER_STATE</p></td>
<td align="left"><p>ACPI は、S 状態に関連付ける D 状態を見つけることができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>マッピングが必要な ACPI 拡張機能</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>マップできない SYSTEM_POWER_STATE</p></td>
<td align="left"><p>システムがこの状態である場合、デバイスはシステムのスリープ状態を解除できることを要求しますが、実際には、この状態がサポートされません。</p></td>
</tr>
</tbody>
</table>

 

パラメーター1が**0x11**の場合、システムは ACPI モードに入ることができませんでした。 この場合、パラメーター2は正確な問題を指定し、残りのパラメーターには次の定義が含まれます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムで AML インタープリターを初期化できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムで RSDT が見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムは、重要なドライバー構造を割り当てることができませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムで RSDT を読み込めませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムで DDBs を読み込めませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムは割り込みベクターに接続できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>SCI_EN は PM1 Control Register では設定されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>無効なチェックサムが含まれているテーブルへのポインター</p></td>
<td align="left"><p>作成者のリビジョン</p></td>
<td align="left"><p>テーブルのチェックサムが正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>ACPI が読み込みに失敗したテーブルへのポインター</p></td>
<td align="left"><p>作成者のリビジョン</p></td>
<td align="left"><p>ACPI が DDB を読み込めませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>FADT のバージョン</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>サポートされていないファームウェアバージョンです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xA</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムは MADT を見つけることができませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xB</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムで、有効なローカル SAPIC 構造体が MADT に見つかりませんでした。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

パラメーター1の値はエラーを示します。

<a name="resolution"></a>解決方法
----------

このエラーをデバッグしている場合は、 [ **! analyze-v**](-analyze.md)拡張機能を使用します。 この拡張機能では、関連するすべてのデータ (デバイスの拡張子、nsobjects、または特定のエラーに適したもの) が表示されます。

デバッグを実行していない場合、このエラーは新しい BIOS を取得する必要があることを示します。 新しい BIOS を入手するには、ベンダーに問い合わせるか、インターネットにアクセスしてください。

BIOS を更新できない場合、または最新の BIOS が ACPI に準拠していない場合は、テキストモードのセットアップ中に ACPI モードをオフにすることができます。 ACPI モードをオフにするには、ストレージドライバーのインストールを確認するメッセージが表示されたら、F7 キーを押します。 システムからは、F7 キーが押されたことが通知されませんが、自動的に ACPI を無効にして、インストールを続行することができます。

<a name="remarks"></a>コメント
-------

Pci ルーティングテーブル (\_PRT) は、すべての pci デバイスを割り込みコントローラーに接続する方法を指定する ACPI BIOS オブジェクトです。 複数の PCI バスがあるコンピューターには\_、複数の prts が存在する場合があります。

デバッガーでは、 \_引数として\_prt オブジェクトのアドレスと共に、 **! acpikd**拡張機能を使用して、prt を表示できます。

 

 




