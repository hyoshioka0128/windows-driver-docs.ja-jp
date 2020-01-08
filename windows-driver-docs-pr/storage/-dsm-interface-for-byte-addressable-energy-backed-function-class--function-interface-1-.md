---
title: JEDEC バイトのアドレス指定可能なエネルギー関数クラスのインターフェイスの _DSM (関数インターフェイス 1)
description: デバイス固有のメソッド (_DSM) インターフェイスは、BIOS の複雑さを最小限に抑えるために、JEDEC バイトのアドレス指定可能なエネルギーサポートインターフェイス標準にマップされるように設計されています。
ms.assetid: 895F1B13-4F2D-4B6B-A3CE-60A8AC9EE7B0
ms.localizationpriority: medium
ms.date: 12/15/2019
ms.openlocfilehash: 9185f1f2f553039682b40e52613f8ddb570d8572
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606528"
---
# <a name="_dsm-interface-for-jedec-byte-addressable-energy-backed-function-class-function-interface-1"></a>JEDEC バイトのアドレス指定可能なエネルギー関数クラスのインターフェイスの _DSM (関数インターフェイス 1)

デバイス固有のメソッド (_DSM) インターフェイスは、BIOS の複雑さを最小限に抑えるために、JEDEC バイトのアドレス指定可能なエネルギーサポートインターフェイス標準にマップされるように設計されています。 これは、デバイスの機能をレポートするための一般的な機能を提供します。これは、OS ソフトウェアが同じメカニズムを使用してさまざまな実装と対話できるようにするための機能 & ます。 さらに、I2C レジスタにアクセスすることによって、ベンダー固有の機能をサポートできます。

_DSM インターフェイスに準拠した、バイトアドレッシング可能なエネルギーサポート関数クラス (関数インターフェイス 1) の場合は、 *JEDEC バイトのアドレス*指定可能なエネルギーサポートインターフェイス仕様 (関数クラス0x01 および関数インターフェイス 0x01) を実装する NVDIMM をサポートできます。 詳細については、 [JEDEC バイトのアドレス指定可能なエネルギーサポートインターフェイス仕様 (ドキュメント JESD245)](https://www.jedec.org/document_search?search_api_views_fulltext=jesd245)を参照してください。

## <a name="_dsm-interface-for-byte-addressable-energy-backed-function-class-function-interface-1"></a>バイトアドレッシング可能なエネルギー対応関数クラスの _DSM インターフェイス1

_DSM GUID は1EE68B36-D4BD-4a1a-9A16-4F8E53D46E05 です。

このセクションで定義されている _DSM 関数は、NVDIMM ACPI 名前空間デバイスオブジェクトに実装する必要があります。 **必須**という用語は、関数が有効なデータを返す必要があるかどうかを示します。

### <a name="mandatory-functions-and-fields"></a>必須の関数とフィールド

次の表に、必須の関数 & フィールドを示します。

| 関数のインデックス | 関数名                                                                                                                                | デバイスで管理されているエネルギーソースポリシーに必須 | ホストによって管理されるエネルギーソースポリシーに必須 |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|------------------------------------------------------|
| 0              | [クエリで実装された関数 (関数インデックス 0)](query-implemented-functions--function-index-0-.md)                                         | [はい]                                                    | [はい]                                                  |
| 1 で保護されたプロセスとして起動されました              | [NVDIMM Id の取得 (関数インデックス 1)](get-nvdimm-n-identification--function-index-1-.md)                                         | [はい]                                                    | [はい]                                                  |
| 2 で保護されたプロセスとして起動されました              | [保存操作の要件を取得する (関数インデックス 2)](get-save-operation-requirements--function-index-2-.md)                                 | [はい]                                                    | [はい]                                                  |
| 3 で保護されたプロセスとして起動されました              | [エネルギーソースの識別を取得する (関数インデックス 3)](get-energy-source-identification--function-index-3-.md)                               | [はい]                                                    | [はい]                                                  |
| ホーム フォルダーが置かれているコンピューターにアクセスできない              | [最後のバックアップ情報の取得 (関数インデックス 4)](get-last-backup-information--function-index-4-.md)                                         | [はい]                                                    | [はい]                                                  |
| 5              | [NVM しきい値の取得 (関数インデックス 5)](get-nvm-thresholds--function-index-5-.md)                                                           | [はい]                                                    | [はい]                                                  |
| 6              | [NVM の有効期間の割合の警告しきい値 (関数インデックス 6)](set-nvm-lifetime-percentage-warning-threshold--function-index-6-.md)     | [はい]                                                    | [はい]                                                  |
| 7              | [エネルギーソースのしきい値を取得する (関数インデックス 7)](get-energy-source-thresholds--function-index-7-.md)                                       | [はい]                                                    | 必須ではない                                                   |
| 8              | [エネルギーソースの有効期間の警告しきい値を設定する (関数インデックス 8)](set-energy-source-lifetime-warning-threshold--function-index-8-.md)       | [はい]                                                    | 必須ではない                                                   |
| 9              | [エネルギーソースの温度の警告しきい値を設定する (関数インデックス 9)](set-energy-source-temperature-warning-threshold--function-index-9-.md) | [はい]                                                    | 必須ではない                                                   |
| 10             | [重大な正常性の情報の取得 (関数インデックス 10)](get-critical-health-info--function-index-10-.md)                                             | [はい]                                                    | [はい]                                                  |
| 11             | [NVDIMM の正常性情報の取得 (関数インデックス 11)](get-nvdimm-n-health-info--function-index-11-.md)                                             | [はい]                                                    | [はい]                                                  |
| 12             | [エネルギーソースの正常性に関する情報の取得 (関数インデックス 12)](get-energy-source-health-info--function-index-12-.md)                                   | [はい]                                                    | 必須ではない                                                   |
| 13             | [操作の統計を取得する (関数インデックス 13)](get-operational-statistics--function-index-13-.md)                                         | [はい]                                                    | [はい]                                                  |
| 14             | [ベンダログページサイズの取得 (関数インデックス 14)](get-vendor-log-page-size--function-index-14-.md)                                             | [はい]                                                    | [はい]                                                  |
| 15             | [ベンダログの取得ページ (関数インデックス 15)](get-vendor-log-page--function-index-15-.md)                                                       | [はい]                                                    | [はい]                                                  |
| 16             | [クエリエラーの挿入状態 (関数インデックス 16)](query-error-injection-status--function-index-16-.md)                                     | [はい]                                                    | [はい]                                                  |
| 17             | [挿入エラー (関数インデックス 17)](inject-error--function-index-17-.md)                                                                     | [はい]                                                    | [はい]                                                  |
| 18             | [挿入したエラーを取得します (関数インデックス 18)](get-injected-errors--function-index-18-.md)                                                       | [はい]                                                    | [はい]                                                  |
| 19             | [NVM イメージの消去 (関数インデックス 19)](erase-nvm-image--function-index-19-.md)                                                               | [はい]                                                    | [はい]                                                  |
| 20             | [Arm NVDIMM-N (関数インデックス 20)](arm-nvdimm-n--function-index-20-.md)                                                                     | [はい]                                                    | [はい]                                                  |
| 21             | [工場出荷時の既定値にリセット (関数インデックス 21)](reset-to-factory-defaults--function-index-21-.md)                                           | [はい]                                                    | [はい]                                                  |
| 22             | [ファームウェア更新の開始 (関数インデックス 22)](start-firmware-update--function-index-22-.md)                                                   | [はい]                                                    | [はい]                                                  |
| 23             | [ファームウェア更新データの送信 (関数インデックス 23)](send-firmware-update-data--function-index-23-.md)                                           | [はい]                                                    | [はい]                                                  |
| 24             | [ファームウェア更新の完了 (関数インデックス 24)](finish-firmware-update--function-index-24-.md)                                                 | [はい]                                                    | [はい]                                                  |
| 25             | [ファームウェアイメージスロットの選択 (関数インデックス 25)](select-firmware-image-slot--function-index-25-.md)                                         | [はい]                                                    | [はい]                                                  |
| 26             | [ファームウェア情報の取得 (関数インデックス 26)](get-firmware-info--function-index-26-.md)                                                           | [はい]                                                    | [はい]                                                  |
| 27             | [I2C 読み取り (関数インデックス 27)](i2c-read--function-index-27-.md)                                                                             | [はい]                                                    | [はい]                                                  |
| 28             | [I2C 書き込み (関数インデックス 28)](i2c-write--function-index-28-.md)                                                                           | [はい]                                                    | [はい]                                                  |
| 29             | [型指定されたデータの読み取り (関数インデックス 29)](read-typed-data--function-index-29-.md)                                                               | [はい]                                                    | [はい]                                                  |
| 30             | [型指定されたデータの書き込み (関数インデックス 30)](write-typed-data--function-index-30-.md)                                                             | [はい]                                                    | [はい]                                                  |
| 31             | [メモリエラーカウンターの設定 (関数インデックス 31)](set-memory-error-counters--function-index-31-.md)                                           | [はい]                                                    | [はい]                                                  |

## <a name="_dsm-method-input"></a>_DSM メソッドの入力

*Arg3*すべての関数は、パッケージ値です。 関数が入力引数を受け取らない場合、パッケージの値にはデータが含まれません。 関数が入力引数を受け取る場合、パッケージの値にはバッファーが含まれます。

関数が入力引数を取らず、 *Arg3*が空のパッケージでない場合、関数は無効な入力パラメーターの**一般ステータスコード**を返します。

## <a name="_dsm-method-output"></a>_DSM メソッドの出力

すべてのメソッドは、4バイト以上の長さのバッファーを返します。 戻りバッファーの最初の4バイトは、次のように構成されます。

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
<th align="left">バイト長</th>
<th align="left">バイト オフセット</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">一般的な状態コード</td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">0</td>
<td align="left"><p>0: 成功</p>
<p>1: サポートされていません。</p>
<p>2–無効な入力パラメーター</p>
<p>3– I2C 通信エラー</p>
<p>4–関数固有のエラーコード</p>
<p>5–ベンダー固有のエラーコード</p>
<p>6-0xFFFF –予約済み</p></td>
</tr>
<tr class="even">
<td align="left">関数固有のエラーコード</td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">2 で保護されたプロセスとして起動されました</td>
<td align="left">このフィールドには、呼び出された関数に固有のエラーコードが含まれています。 このフィールドには、<strong>一般ステータスコード</strong>が<strong>関数固有のエラーコード</strong>と同じ場合にのみ有効な情報が含まれます。</td>
</tr>
<tr class="odd">
<td align="left">ベンダー固有のエラーコード</td>
<td align="left">1 で保護されたプロセスとして起動されました</td>
<td align="left">3 で保護されたプロセスとして起動されました</td>
<td align="left">このフィールドには、ベンダー固有の状態コードが含まれています。 <strong>一般ステータスコード</strong>が<strong>ベンダー固有のエラーコード</strong>と等しい場合にのみ、有効な情報が含まれます。</td>
</tr>
</tbody>
</table>

0以外の**一般的な状態コード**は、関数が失敗したことを示します。 このバージョンの仕様で定義されている関数は、サポートされ**ていない** **一般的な状態コード**を返す必要があります。 すべての必須関数は、有効なデータまたはランタイムエラーを示すエラーコードを返す必要があります。 必須ではない関数は、返される有効なデータがないことを通知するために、関数固有のエラーコードを返す場合があります。

予約されているすべてのビットとバイトは、値が0である必要があります。 特に明記されていない限り、すべてのマルチバイトフィールドはリトルエンディアン方式で表現する必要があります。

> [!NOTE]
> このインターフェイスで指定されている関数の多くの戻り値フィールドは、型指定可能なエネルギーベースのインターフェイスレジスタへの参照によって記述されます。 これらのフィールドは、"バイトアドレス可能なエネルギーサポートインターフェイス、バージョン1.0、JEDEC Standard No" で定義されているレジスタと同じである必要があります。 2233-22 "バイトアドレス可能なエネルギーベースのインターフェイス仕様のリビジョン。 仕様バージョンは、 [GET NVDIMM-N id (関数インデックス 1)](get-nvdimm-n-identification--function-index-1-.md)関数によって返される**仕様リビジョン**フィールドで報告されます。
>
> 一部のリターンフィールドは、エネルギーソースに関する情報を参照します。 ES ポリシーがデバイスで管理されている場合、プラットフォームは、フィールドの説明で指定されているハードウェアレジスタを読み取って、すべての ES 関連情報を取得します。 ES ポリシーがホストによって管理されている場合、プラットフォーム固有のメカニズムを通じて ES 関連の情報を取得する必要があります。 この場合、すべての ES 関連情報は、フィールドの説明で指定されたハードウェアレジスタと同じバイナリレイアウトで表示されます。
