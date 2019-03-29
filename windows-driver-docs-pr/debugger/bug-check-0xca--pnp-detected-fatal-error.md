---
title: Bug Check 0xCA PNP_DETECTED_FATAL_ERROR
description: PNP_DETECTED_FATAL_ERROR のバグ チェックでは、0x000000CA の値を持ちます。 これは、プラグ アンド プレイのマネージャーに重大なエラーが発生したことを示します。
ms.assetid: 2092c4a7-e068-461f-b28e-8063faf5a031
keywords:
- Bug Check 0xCA PNP_DETECTED_FATAL_ERROR
- PNP_DETECTED_FATAL_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PNP_DETECTED_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd43204409e9ab7b41df36c708aa9173c7af3355
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349929"
---
# <a name="bug-check-0xca-pnpdetectedfatalerror"></a>バグ チェック 0xCA:PNP\_検出\_FATAL\_エラー


PNP\_検出\_FATAL\_エラーのバグ チェックが 0x000000CA の値を持ちます。 これは、プラグ アンド プレイのマネージャーにおそらく問題のあるプラグ アンド プレイ ドライバーの結果として、重大なエラーが発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="pnpdetectedfatalerror-parameters"></a>PNP\_検出\_FATAL\_エラー パラメーター


パラメーター 1 では、違反の種類を識別します。

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
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>新たに報告された PDO のアドレス</p></td>
<td align="left"><p>重複していますが、古い PDO のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong>PDO が重複しています。</strong>ドライバーの特定のインスタンスが同じデバイス ID と一意の Id で複数の Pdo を列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>PDO の人物のアドレス</p></td>
<td align="left"><p>ドライバー オブジェクトのアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong>無効な PDO:</strong>ランダムなメモリ、または、FDO または初期化されていない PDO PDO を必要とする API が呼び出されました。</p>
<p>(プラグ アンド プレイによってを返されませんが、初期化されていない PDO は<strong>QueryDeviceRelation</strong>または<strong>QueryBusRelations</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>PDO の Id を持つクエリの対象のアドレス</p></td>
<td align="left"><p>ID のバッファーのアドレス</p></td>
<td align="left"><p><strong>1:</strong>DeviceID</p>
<p><strong>2:</strong>一意の Id</p>
<p><strong>3:</strong>HardwareIDs</p>
<p><strong>4:</strong>CompatibleIDs</p></td>
<td align="left"><p><strong>ID が無効です。</strong>列挙子には、無効な文字を含む、または正しく終了していない ID が返されます。 (Id を含める必要がありますから 0x7f までの範囲 0x20-0x2B と 0x2D - でのみ文字します)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>DOE_DELETE_PENDING で PDO のアドレスの設定</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong>削除済みの PDO の無効な列挙型は:</strong>列挙子がこれを使用していた以前削除 PDO を返される<strong>IoDeleteDevice</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>PDO のアドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong>解放 devnode ツリーでリンクされているときに PDO:</strong>Devnode まだツリー リンクされた中には、0 に削除された PDO のオブジェクトのマネージャー参照数。 (これは通常示しますエントリのクエリ IRP の PDO を返すときに、ドライバーは、参照が追加されません。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>スタックにバスの無効な関係が返される PDO のアドレス</p></td>
<td align="left"><p>Pdo の合計数は、bus 関係として返されます</p></td>
<td align="left"><p>位置 (0 から始まる) インデックス最初<strong>NULL</strong> PDO が見つかりました</p></td>
<td align="left"><p><strong>バス関係として NULL ポインターが返されます。</strong>1 つまたは複数のデバイス、バス上に存在するが、 <strong>NULL</strong> PDO します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>渡された接続の種類</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong>無効な接続の種類は、IoDisconnectInterruptEx に渡されます。</strong>ドライバーが、無効な接続型を渡された<strong>IoDisconnectInterruptEx</strong>します。 このルーチンに渡される接続の種類が対応する正常な呼び出しで返されると一致する必要があります<strong>IoConnectInterruptEx</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xa</p></td>
<td align="left"><p>ドライバー オブジェクト</p></td>
<td align="left"><p>ドライバーのコールバックから戻った後 IRQL</p></td>
<td align="left"><p>ドライバーのコールバックから戻る APC 無効にするカウントの合計</p></td>
<td align="left"><p><strong>正しくないは、コールバック動作を通知します。</strong>ドライバーは IRQL を保持するために失敗したか、APC の無効化の数に結合して、プラグ 'n' 通知を再生します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>関連 PDO</p></td>
<td align="left"><p>リレーションの削除</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p><strong>削除済みの PDO は、関係として報告されます。</strong>削除するデバイスの削除の関係のいずれかが既に削除されました。</p></td>
</tr>
</tbody>
</table>

 

 

 




