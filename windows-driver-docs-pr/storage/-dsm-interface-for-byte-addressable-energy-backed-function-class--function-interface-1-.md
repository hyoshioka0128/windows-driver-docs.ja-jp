---
title: '\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ'
description: このインターフェイスは、BIOS の複雑さを軽減するために、JEDEC バイト アドレス指定可能なエネルギー バックアップ インターフェイス マップに設計されています。
ms.assetid: 895F1B13-4F2D-4B6B-A3CE-60A8AC9EE7B0
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ad64fa2cd12d9b0dadcb63d034e9c09dc7109f5d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382753"
---
# <a name="dsm-interface-for-byte-addressable-energy-backed-function-class-function-interface-1"></a>\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ


このインターフェイスは、BIOS の複雑さを軽減するために、JEDEC バイト アドレス指定可能なエネルギー バックアップ インターフェイス マップに設計されています。 OS ソフトウェアが同じメカニズムを通じてさまざまな実装が操作できるよう、デバイスの機能と機能、レポートの共通の基盤を提供します。 さらに、I2C レジスタへのアクセスによりベンダー固有の機能をサポートできます。

プラットフォームに準拠する\_DSM クラスのインターフェイスをバイト アドレス指定可能なエネルギー バックアップ関数 (関数のインターフェイスの 1) を実装する NVDIMM-N をサポートできる、 *JEDEC バイト アドレス指定可能なエネルギー バックアップ インターフェイス*(0x01 の関数クラスと関数インターフェイス 0x01) を指定します。 詳細については、次を参照してください。、 [JEDEC バイト アドレス指定可能なエネルギー バックアップ Interface specification (ドキュメント JESD245)](https://www.jedec.org/document_search?search_api_views_fulltext=jesd245)します。

## <a name="span-iddsminterfaceforbyteaddressableenergybackedfunctionclassfunctioninterface1spanspan-iddsminterfaceforbyteaddressableenergybackedfunctionclassfunctioninterface1spanspan-iddsminterfaceforbyteaddressableenergybackedfunctionclassfunctioninterface1spandsm-interface-for-byte-addressable-energy-backed-function-class-function-interface-1"></a><span id="DSM_Interface_for_Byte_Addressable_Energy_Backed_Function_Class_Function_Interface_1"></span><span id="dsm_interface_for_byte_addressable_energy_backed_function_class_function_interface_1"></span><span id="DSM_INTERFACE_FOR_BYTE_ADDRESSABLE_ENERGY_BACKED_FUNCTION_CLASS_FUNCTION_INTERFACE_1"></span>\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス バックアップ関数クラス、関数のインターフェイス 1


\_DSM GUID は 1EE68B36-D4BD-4a1a-9A16-4F8E53D46E05 します。

\_NVDIMM ACPI Namespace デバイス オブジェクトでこのドキュメントで定義されている DSM 関数を実装するものとします。 用語**必須**かどうかする必要がありますを返す有効なデータかどうかを参照します。

### <a name="span-idmandatoryfunctionsandfieldsspanspan-idmandatoryfunctionsandfieldsspanspan-idmandatoryfunctionsandfieldsspanmandatory-functions-and-fields"></a><span id="Mandatory_functions_and_fields"></span><span id="mandatory_functions_and_fields"></span><span id="MANDATORY_FUNCTIONS_AND_FIELDS"></span>必須の関数およびフィールド

次の表では、関数および必須のフィールドを指定します。

| 関数インデックス | 関数名                                                                                                                                | デバイスで管理されたエネルギー ソース (ES) ポリシーでは必須 | 管理されているホストのエネルギー ソース (ES) ポリシーでは必須 |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|------------------------------------------------------|
| 0              | [実装済み関数 (関数のインデックス 0) のクエリします。](query-implemented-functions--function-index-0-.md)                                         | 〇                                                    | 〇                                                  |
| 1              | [NVDIMM-N 識別 (関数インデックス 1) を取得します。](get-nvdimm-n-identification--function-index-1-.md)                                         | 〇                                                    | 〇                                                  |
| 2              | [保存操作の要件 (関数インデックス 2) を取得します。](get-save-operation-requirements--function-index-2-.md)                                 | 〇                                                    | 〇                                                  |
| 3              | [エネルギー ソースの識別 (関数インデックス 3) を取得します。](get-energy-source-identification--function-index-3-.md)                               | 〇                                                    | 〇                                                  |
| 4              | [最後のバックアップ情報 (関数インデックス 4) を取得します。](get-last-backup-information--function-index-4-.md)                                         | 〇                                                    | 〇                                                  |
| 5              | [NVM のしきい値 (関数インデックス 5) を取得します。](get-nvm-thresholds--function-index-5-.md)                                                           | 〇                                                    | 〇                                                  |
| 6              | [NVM の有効期間率の警告しきい値 (関数のインデックス 6) の設定します。](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)     | 〇                                                    | 〇                                                  |
| 7              | [エネルギー ソースしきい値 (関数インデックス 7) を取得します。](get-energy-source-thresholds--function-index-7-.md)                                       | 〇                                                    | X                                                   |
| 8              | [エネルギーのソースの有効期間の警告しきい値 (関数インデックス 8) の設定します。](set-energy-source-lifetime-warning-threshold--function-index-8-.md)       | 〇                                                    | X                                                   |
| 9              | [エネルギー ソース温度の警告しきい値 (関数インデックス 9) の設定します。](set-energy-source-temperature-warning-threshold--function-index-9-.md) | 〇                                                    | X                                                   |
| 10             | [重要な正常性の情報 (関数インデックス 10) を取得します。](get-critical-health-info--function-index-10-.md)                                             | 〇                                                    | 〇                                                  |
| 11             | [NVDIMM-N の正常性の情報 (関数インデックス 11) を取得します。](get-nvdimm-n-health-info--function-index-11-.md)                                             | 〇                                                    | 〇                                                  |
| 12             | [エネルギー ソース ヘルス情報 (関数インデックス 12) を取得します。](get-energy-source-health-info--function-index-12-.md)                                   | 〇                                                    | X                                                   |
| 13             | [(関数インデックス 13) の運用統計を取得します。](get-operational-statistics--function-index-13-.md)                                         | 〇                                                    | 〇                                                  |
| 14             | [仕入先ログ ページ サイズ (関数インデックス 14) を取得します。](get-vendor-log-page-size--function-index-14-.md)                                             | 〇                                                    | 〇                                                  |
| 15             | [仕入先ログ ページ (関数インデックス 15) を取得します。](get-vendor-log-page--function-index-15-.md)                                                       | 〇                                                    | 〇                                                  |
| 16             | [クエリ エラーの挿入の状態 (関数インデックス 16)](query-error-injection-status--function-index-16-.md)                                     | 〇                                                    | 〇                                                  |
| 17             | [エラー (関数インデックス 17) を挿入します。](inject-error--function-index-17-.md)                                                                     | 〇                                                    | 〇                                                  |
| 18             | [挿入されたエラー (関数インデックス 18) の取得](get-injected-errors--function-index-18-.md)                                                       | 〇                                                    | 〇                                                  |
| 19             | [消去 NVM イメージ (関数インデックス 19)](erase-nvm-image--function-index-19-.md)                                                               | 〇                                                    | 〇                                                  |
| 20             | [Arm の Nvdimm-n (関数インデックス 20)](arm-nvdimm-n--function-index-20-.md)                                                                     | 〇                                                    | 〇                                                  |
| 21             | [設定にリセットして既定値は (関数インデックス 21)](reset-to-factory-defaults--function-index-21-.md)                                           | 〇                                                    | 〇                                                  |
| 22             | [ファームウェア更新を開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)                                                   | 〇                                                    | 〇                                                  |
| 23             | [ファームウェアの更新データ (関数インデックス 23) の送信します。](send-firmware-update-data--function-index-23-.md)                                           | 〇                                                    | 〇                                                  |
| 24             | [ファームウェアの更新 (関数インデックス 24) の完了します。](finish-firmware-update--function-index-24-.md)                                                 | 〇                                                    | 〇                                                  |
| 25             | [ファームウェア イメージのスロット (25 のインデックス関数) を選択します。](select-firmware-image-slot--function-index-25-.md)                                         | 〇                                                    | 〇                                                  |
| 26             | [ファームウェア情報 (関数インデックス 26) を取得します。](get-firmware-info--function-index-26-.md)                                                           | 〇                                                    | 〇                                                  |
| 27             | [I2C 読み取り (関数インデックス 27)](i2c-read--function-index-27-.md)                                                                             | 〇                                                    | 〇                                                  |
| 28             | [I2C 書き込み (関数インデックス 28)](i2c-write--function-index-28-.md)                                                                           | 〇                                                    | 〇                                                  |
| 29             | [型指定されたデータ (関数インデックス 29) の読み取り](read-typed-data--function-index-29-.md)                                                               | 〇                                                    | 〇                                                  |
| 30             | [型指定されたデータ (関数インデックス 30) の書き込み](write-typed-data--function-index-30-.md)                                                             | 〇                                                    | 〇                                                  |
| 31             | [メモリ エラー カウンター (関数インデックス 31) の設定します。](set-memory-error-counters--function-index-31-.md)                                           | 〇                                                    | 〇                                                  |

 

## <a name="span-iddsmmethodinputspanspan-iddsmmethodinputspandsm-method-input"></a><span id="DSM_METHOD_INPUT"></span><span id="dsm_method_input"></span>\_DSM メソッドの入力


*Arg3*すべての関数には、パッケージの値。 関数が入力引数を受け取らない場合、パッケージの値にデータがないです。 関数が入力引数を受け取る場合、パッケージの値には、バッファーが含まれています。

関数は入力引数を受け取らない場合と*Arg3*は空のパッケージは、関数を返します、**一般的なステータス コード**の無効な入力パラメーター。

## <a name="dsm-method-output"></a>\_DSM メソッドの出力


すべてのメソッドは 4 バイト以上の長さのバッファーを返します。 戻り値のバッファーの最初の 4 バイトの構造は次のとおりです。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">フィールド</th>
<th align="left">バイトの長さ</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">[全般] の状態コード</td>
<td align="left">2</td>
<td align="left">0</td>
<td align="left"><p>0-成功</p>
<p>1 – サポートされていない</p>
<p>2 – 無効な入力パラメーター</p>
<p>3 – I2C 通信エラー</p>
<p>4 – 関数に固有のエラー コード</p>
<p>5 – ベンダー固有のエラー コード</p>
<p>6-0 xffff – に予約されています</p></td>
</tr>
<tr class="even">
<td align="left">関数に固有のエラー コード</td>
<td align="left">1</td>
<td align="left">2</td>
<td align="left">このフィールドには、呼び出された関数に固有のエラー コードが含まれています。 このフィールドは、場合のみ有効な情報を含む<strong>一般的なステータス コード</strong>と等しい<strong>関数に固有のエラー コード</strong>。</td>
</tr>
<tr class="odd">
<td align="left">ベンダー固有のエラー コード</td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left">このフィールドには、ベンダー固有の状態コードが含まれています。 場合のみ有効な情報を含む、<strong>一般的なステータス コード</strong>と等しい<strong>ベンダー固有のエラー コード</strong>します。</td>
</tr>
</tbody>
</table>

 

0 以外の任意**一般的なステータス コード**関数が失敗したことを示します。 このバージョンの仕様で定義された関数が返されないものと、**一般的なステータス コード**の**はサポートされていません**します。 すべての必須の関数は有効なデータまたはランタイム エラーを示すエラー コードを返します。 非必須関数は、返される有効なデータがないことを通知する関数に固有のエラー コードを返す可能性があります。

すべての予約済みビットやバイトは 0 の値を持ちます。 具体的には特に明記しない限り、マルチ バイトのすべてのフィールドはリトル エンディアンの方法で表されるものとします。

&gt; \[!注\]    &gt;Byte Addressable Energy-Backed インターフェイス レジスタへの参照がこのインターフェイスで指定された関数の多くの戻り値のフィールドについて説明します。 これらのフィールドはインターフェイスで定義された、"バイト アドレス指定可能なエネルギー バックアップ、バージョン 1.0、JEDEC 標準いいえ。 登録に同一であります。 2233-22"Byte-Addressable Energy-Backed インターフェイスの仕様のリビジョン。 仕様のバージョンが報告された、**仕様のリビジョン**によって返されるフィールド、 [NVDIMM-N の Id を取得する (関数インデックス 1)](get-nvdimm-n-identification--function-index-1-.md)関数。

&gt;いくつかを返すフィールドをエネルギー ソース (ES) についての情報を参照してください。 ES ポリシーは、デバイス管理は、プラットフォーム、ES に関連するすべての情報を取得するフィールドの説明で指定されたハードウェア レジスタが読み取られます。 ES ポリシーは、管理されているホストが、プラットフォームはプラットフォーム固有のメカニズムを使用、ES 関連の情報を取得します。 ハードウェアと同じバイナリ レイアウトで ES に関連するすべての情報を表示するものとここでは、フィールドの説明で指定された登録します。

&gt;

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[ストレージ ドライバーの設計ガイド](https://go.microsoft.com/fwlink/p/?LinkId=798409)

[JEDEC バイトのアドレス指定可能なエネルギー バックアップ インターフェイス NVDIMM デバイス固有のメソッド (\_DSM)](jedec-byte-addressable-energy-backed-interface-nvdimms-device-specific-method---dsm-.md)

 

 






