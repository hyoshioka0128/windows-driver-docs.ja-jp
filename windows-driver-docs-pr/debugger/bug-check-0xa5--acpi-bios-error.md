---
title: バグ チェック 0xA5 ACPI_BIOS_ERROR
description: ACPI_BIOS_ERROR のバグ チェックでは、コンピューターの ACPI BIOS が ACPI 仕様に完全に準拠していないことを示す 0x000000A5 の値を持ちます。
ms.assetid: f0366a3c-a2c4-4fc8-a722-52fdda59eb2b
keywords:
- バグ チェック 0xA5 ACPI_BIOS_ERROR
- ACPI_BIOS_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ACPI_BIOS_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1ad38b67e5b2ed8e8c218c32a442be33013c6a89
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903800"
---
# <a name="bug-check-0xa5-acpibioserror"></a>バグ チェック 0xA5:ACPI\_BIOS\_エラー


ACPI\_BIOS\_エラーのバグ チェックが 0x000000A5 の値を持ちます。 このバグ チェックでは、コンピューターの Advanced Configuration and Power Interface (ACPI) BIOS が ACPI の仕様に完全準拠ではないことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="acpibioserror-parameters"></a>ACPI\_BIOS\_エラー パラメーター


パラメーター 1 では、非互換性の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

プラグ アンド プレイ (PnP) または電源の管理には、BIOS の非互換性が関連付けられている場合は、次のパラメーターが使用されます。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>ACPI の<strong>deviceExtension</strong></p></td>
<td align="left"><p>ACPI の<strong>ResourceList</strong></p></td>
<td align="left"><p><strong>0:</strong>リソースの一覧が見つかりません</p>
<p><strong>1:</strong>一覧に IRQ リソースが見つかりません</p></td>
<td align="left"><p>ACPI は、ACPI の開始時に渡されるリソースのシステム コントロールの割り込み (SCI) のベクターを見つけることはできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(参照の表に、後でこのページ)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>ACPI オブジェクトが実行されています。</p></td>
<td align="left"><p>インタープリターからの戻り値</p></td>
<td align="left"><p>(ULONG 形式) でのコントロールのメソッドの名前</p></td>
<td align="left"><p>ACPI を ACPI 名前空間を表すデバイスの拡張機能を作成するときにコントロールのメソッドを実行しようとしましたが、このコントロールのメソッドが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>その _PRW が属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p><strong>DataType</strong> (Amli.h を参照してください) が返されます</p></td>
<td align="left"><p>ACPI は、_PRW を評価し、パッケージ要素として整数が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>その _PRW が属する ACPI 拡張機能</p></td>
<td align="left"><p>_PRW Aointer</p></td>
<td align="left"><p>_PRW 内の要素の数</p></td>
<td align="left"><p>ACPI は、_PRW、およびパッケージを少なくとも 2 つの要素を含めることができませんでした届きました評価されます。 ACPI の仕様では、2 つの要素が存在する _PRW する常にある必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>その _PRx が属する ACPI 拡張機能</p></td>
<td align="left"><p>_PRx へのポインター</p></td>
<td align="left"><p>検索するオブジェクトの名前へのポインター</p></td>
<td align="left"><p>ACPI は、名前付きオブジェクトを検索しようとしていますが、オブジェクトが見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p><strong>DataType</strong> (Amli.h を参照してください) が返されます</p></td>
<td align="left"><p>ACPI は、メソッドを評価し、戻り値のバッファーを受信することにします。 ただし、メソッドには、他のデータ型が返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p><strong>DataType</strong> (Amli.h を参照してください) が返されます</p></td>
<td align="left"><p>ACPI は、メソッドを評価し、戻り値の整数を受け取ることを想定します。 ただし、メソッドには、他のデータ型が返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p><strong>DataType</strong> (Amli.h を参照してください) が返されます</p></td>
<td align="left"><p>ACPI は、メソッドを評価し、代わりに、パッケージを受信することにします。 ただし、メソッドには、他のデータ型が返されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>メソッドが属する ACPI 拡張機能</p></td>
<td align="left"><p>メソッドへのポインター</p></td>
<td align="left"><p><strong>DataType</strong> (Amli.h を参照してください) が返されます</p></td>
<td align="left"><p>ACPI は、メソッドを評価し、文字列を取得するが必要です。 ただし、メソッドには、他のデータ型が返されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>その _EJD が属する ACPI 拡張機能</p></td>
<td align="left"><p>インタープリターが返すステータス</p></td>
<td align="left"><p>ACPI は、検索を試行しているオブジェクトの名前</p></td>
<td align="left"><p>ACPI は、_EJD 文字列が参照するオブジェクトを見つけることができません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ACPI のドッキング ステーション デバイスの検出、ACPI 拡張機能</p></td>
<td align="left"><p>_EJD メソッドへのポインター</p></td>
<td align="left"><p><strong>0:</strong>BIOS では、システムが dockage は主張しません</p>
<p><strong>1:</strong>ドッキング ステーション デバイスのデバイスの拡張機能が重複しています</p></td>
<td align="left"><p>ACPI は、ドック サポートの問題があるかが不足している情報を提供します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ACPI のオブジェクトを必要がある、ACPI 拡張機能</p></td>
<td align="left"><p>ACPI 検索メソッドの名前 (ULONG)</p></td>
<td align="left"><p><strong>0:</strong>基本的な事例</p>
<p><strong>1:</strong>Conflict</p></td>
<td align="left"><p>ACPI 見つかりませんでした。 必要なメソッドやオブジェクト _HID または _ADR の存在が存在しない場合、このバグ チェック コードが使用される名前空間。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>NS <strong>PowerResource</strong> ACPI のオブジェクトが必要とします。</p></td>
<td align="left"><p>ACPI 検索メソッドの名前 (ULONG)</p></td>
<td align="left"><p>0:基本的な事例</p></td>
<td align="left"><p>ACPI が見つかりませんでした必要なメソッドやオブジェクト、名前空間での電源のリソース (または「デバイス」以外のエンティティ)。 このバグ チェック コードは、_ON、_OFF、または _STA power リソースの存在がない場合に使用されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>ACPI の解析が現在のバッファー</p></td>
<td align="left"><p>バッファーのタグ</p></td>
<td align="left"><p>指定したバッファーの長さ</p></td>
<td align="left"><p>ACPI は、リソースの記述子を解析できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(参照の表に、後でこのページ)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>(参照の表に、後でこのページ)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ACPI の解析が現在のバッファー</p></td>
<td align="left"><p>バッファーのタグ</p></td>
<td align="left"><p>バッファーの ULONGLONG 長さを格納する変数へのポインター</p></td>
<td align="left"><p>ACPI は、リソースの記述子を解析できませんでした。 長さは、MAXULONG を超えています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ACPI 機械語 (AML) コンテキスト</p></td>
<td align="left"><p><strong>1:</strong>テーブルの読み込みに失敗しました</p>
<p><strong>2:</strong>パラメーターのパスの文字列オブジェクトが見つかりませんでした。</p>
<p><strong>3:</strong>ParameterPath 文字列オブジェクトにパラメーターのデータを挿入できませんでした。</p>
<p><strong>4:</strong>システム メモリが不足</p></td>
<td align="left"><p>NT 状態コード</p></td>
<td align="left"><p>ACPI は、テーブルの読み込みを試みるときに致命的なエラーがありました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>親 NSOBJ へのポインター</p></td>
<td align="left"><p>無効な子 ACPI 名前空間のオブジェクトへのポインター</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ACPI は、xSDT を処理するときに致命的なエラーがありました。 オブジェクトは、子を持つことができない parent の子として宣言されました。</p></td>
</tr>
</tbody>
</table>

 

割り込みのルーティングの障害または互換性の問題が発生した場合は、次のパラメーターが使用されます。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p><strong>InterruptModel</strong> (integer)</p></td>
<td align="left"><p>インタープリターからの戻り値</p></td>
<td align="left"><p>PIC コントロールのメソッドへのポインター</p></td>
<td align="left"><p>ACPI は PIC 制御方法を評価しようとしましたが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10001</p></td>
<td align="left"><p>デバイス オブジェクトへのポインター</p></td>
<td align="left"><p>デバイス オブジェクトの親へのポインター</p></td>
<td align="left"><p>_PRT オブジェクトへのポインター</p>
<p>(次のコメント セクションを参照してください)</p></td>
<td align="left"><p>ACPI は、ルーティング、割り込み実行しようとしましたが失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10002</p></td>
<td align="left"><p>デバイス オブジェクトへのポインター</p></td>
<td align="left"><p>ACPI が求めていたが見つかりませんでした。 文字列名へのポインター</p></td>
<td align="left"><p>_PRT オブジェクトへのポインター</p>
<p>(次のコメント セクションを参照してください)</p></td>
<td align="left"><p>ACPI は、_PRT で参照されているリンクのノードを見つけられませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10003</p></td>
<td align="left"><p>デバイス オブジェクトへのポインター</p></td>
<td align="left"><p>デバイスの ID または関数番号。</p>
<p>この dword 値は次のようにエンコードされますビット 5:0 は PCI デバイス番号、および bits 8:6 は PCI 関数の数。</p></td>
<td align="left"><p>_PRT オブジェクトへのポインター</p>
<p>(次のコメント セクションを参照してください)</p></td>
<td align="left"><p>ACPI が見つかりませんでしたマッピング _PRT パッケージ内のデバイス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10005</p></td>
<td align="left"><p>_PRT オブジェクトへのポインター</p>
<p>(次のコメント セクションを参照してください)</p></td>
<td align="left"><p>現在の _PRT 要素へのポインター。</p>
<p>(このポインターは、_PRT へのインデックスです)。</p></td>
<td align="left"><p>デバイスの ID または関数番号。</p>
<p>この dword 値は次のようにエンコードされますビット 15:0 は、PCI 関数番号であり、ビット 31:16 は PCI デバイス数。</p></td>
<td align="left"><p>ACPI は、関数の ID がないためのすべての F _PRT でエントリを検出します。</p>
<p>(_PRT エントリの一般的な形式はデバイス番号を指定すると、関数の数ではありませんが)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10006</p></td>
<td align="left"><p>リンク ノードへのポインター。</p>
<p>(このデバイスにメソッドがない _DIS。)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI 見つかったリンクのノードが、ノードが無効にすることはできません。</p>
<p>(リンクのノードは再プログラミングのために無効する必要があります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10007</p></td>
<td align="left"><p>ベクターが見つかりませんでした。</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>_PRT には、I/O APIC のエントリの MAPIC テーブルに記述されていないベクターへの参照が含まれています。</p></td>
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
<td align="left"><p>固定の ACPI 記述テーブル (FADT) が見つかりませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1000A</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ルートのシステムの説明のポインター (RSDP) または拡張システムの説明テーブル (XSDT) を配置できませんでした。</p>
<p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1000B</p></td>
<td align="left"><p>ACPI テーブルの署名</p></td>
<td align="left"><p>ACPI テーブルへのポインター</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI テーブルの長さは、テーブルのリビジョンに一貫性がありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000</p></td>
<td align="left"><p>固定の表に、I/O ポート</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>固定の ACPI 記述テーブルで PM_TMR_BLK エントリは、作業の ACPI タイマー ブロックを指していません。</p></td>
</tr>
</tbody>
</table>

 

その他の失敗または互換性の問題が発生した場合は、次のパラメーターが使用されます。

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
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x20000</p></td>
<td align="left"><p>固定の表に、I/O ポート</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>固定の ACPI 記述テーブルで PM_TMR_BLK エントリは、作業 ACPI タイマー ブロックには指していません。</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 と等しい場合**0x02**、ACPI BIOS は、ルートの PCI バスのリソースの一覧を処理できませんでした。 ここでは、パラメーター 3 が、正確な問題を指定し、残りのパラメーターは、次の定義を指定します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PCI バスの ACPI 拡張機能</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>QUERY_RESOURCES IRP へのポインター</p></td>
<td align="left"><p>ACPI は、BIOS のリソースの一覧を適切な形式に変換することはできません。 おそらく、これは、BIOS の一覧のエンコーディングの手順でエラーを表します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCI バスの ACPI 拡張機能</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>QUERY_RESOURCE_REQUIREMENTS IRP へのポインター</p></td>
<td align="left"><p>ACPI は、BIOS のリソースの一覧を適切な形式に変換することはできません。 おそらく、これは、BIOS の一覧のエンコーディングの手順でエラーを表します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCI バスの ACPI 拡張機能</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>ACPI は、空のリソース一覧が見つかりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PCI バスの ACPI 拡張機能</p></td>
<td align="left"><p>0x3</p></td>
<td align="left"><p>PNP CRS 記述子へのポインター</p></td>
<td align="left"><p>ACPI は、CRS の現在のバス番号を見つけられませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PCI バスの ACPI 拡張機能</p></td>
<td align="left"><p>PCI のリソースの一覧へのポインター</p></td>
<td align="left"><p>E820 メモリ テーブルへのポインター</p></td>
<td align="left"><p>PCI の要求をデコードするリソースの一覧は、メモリ領域の E820 BIOS がレポートをインターフェイスの一覧と重複します。 (この種の競合は許可されません)</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 と等しい場合**0x10**、ACPI BIOS は、システムに、デバイスの状態マッピングが正しくを特定できませんでした。 このような状況では、パラメーター 3 が、正確な問題を指定し、残りのパラメーターは、次の定義を持ちます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>そのマッピングが必要な ACPI 拡張機能</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>DEVICE_POWER_STATE (これは、「x + 1」)</p></td>
<td align="left"><p>サポートされていない S 状態に戻す _PRx がマップされていた。</p></td>
</tr>
<tr class="even">
<td align="left"><p>そのマッピングが必要な ACPI 拡張機能</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>マップできない SYSTEM_POWER_STATE</p></td>
<td align="left"><p>ACPI は、S 状態に関連付ける D 状態を見つけることができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>そのマッピングが必要な ACPI 拡張機能</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>マップできない SYSTEM_POWER_STATE</p></td>
<td align="left"><p>デバイスは、システムがこの S 状態が、システムは実際にこの S の状態をサポートしていません、システムをスリープ解除することを要求します。</p></td>
</tr>
</tbody>
</table>

 

パラメーター 1 と等しい場合**パターン**システムでは、ACPI モードは移行できませんでした。 このような状況では、パラメーター 2 が、正確な問題を指定し、残りのパラメーターは、次の定義を持ちます。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムは、AML インタープリターを初期化できませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>RSDT は見つかりませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムは、不可欠なドライバー構造体を割り当てられませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムでは、RSDT を読み込むことができません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x4</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムでは、Ddb を読み込むことができません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x5</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムは、割り込みのベクターに接続できません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x6</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>SCI_EN は、PM1 コントロールの登録の設定になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>不適切なチェックサムのあるテーブルへのポインター</p></td>
<td align="left"><p>作成者改訂番号</p></td>
<td align="left"><p>テーブルのチェックサムが正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>ACPI は、読み込みに失敗したテーブルへのポインター</p></td>
<td align="left"><p>作成者改訂番号</p></td>
<td align="left"><p>ACPI は、DDB を読み込めませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>FADT バージョン</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>サポートされていないファームウェアのバージョン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>MADT は見つかりませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>システムで MADT の有効なローカル SAPIC 構造体が見つかりませんでした。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

パラメーター 1 の値は、エラーを示します。

<a name="resolution"></a>解決方法
----------

このエラーをデバッグしている場合は、使用、 [ **! 分析-v** ](-analyze.md)拡張機能。 この拡張機能では、すべての関連データ (デバイスの拡張機能、nsobjects、または特定のエラーに適した) が表示されます。

デバッグを実行していない場合、このエラーは、新しい BIOS を取得するがあることを示します。 ベンダに問い合わせて、または新しい BIOS を取得する、インターネットにアクセスしてください。

取得できない場合、BIOS の更新または最新の BIOS は引き続きいない ACPI に準拠して、テキスト モードのセットアップ中に、ACPI モードをオフにすることができます。 ACPI モードをオフにするには、ストレージ ドライバーのインストールを求められたら、F7 キーを押します。 システム通知は表示されません、F7 キーが押されましたが、ACPI を無効にし、インストールを続行することができますが、サイレント モードでします。

<a name="remarks"></a>注釈
-------

PCI のルーティング テーブル (\_PRT)、ACPI BIOS オブジェクトを指定するには、すべての PCI デバイスは割り込みコント ローラーに接続する方法。 複数の PCI バスを使用しているコンピューターが複数あります\_Prt します。

表示することができます、 \_PRT を使用してデバッガーで、 **! acpikd.nsobj**のアドレスと共に拡張機能、 \_PRT オブジェクトを引数として。

 

 




