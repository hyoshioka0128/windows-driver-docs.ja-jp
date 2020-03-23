---
title: 'バグ チェック 0x13A: KERNEL_MODE_HEAP_CORRUPTION'
description: KERNEL_MODE_HEAP_CORRUPTION バグ チェックの値は、0x0000013A です。 これは、カーネル モード ヒープ マネージャーがヒープ内で破損を検出したことを示します。
ms.assetid: 806669B3-B811-462A-A3B6-2F583BF0E19A
keywords:
- 'バグ チェック 0x13A: KERNEL_MODE_HEAP_CORRUPTION'
- KERNEL_MODE_HEAP_CORRUPTION
ms.date: 02/14/2020
topic_type:
- apiref
api_name:
- KERNEL_MODE_HEAP_CORRUPTION
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: 986f5e5684c586579ca6766c8b114eae58affac0
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402352"
---
# <a name="bug-check-0x13a-kernel_mode_heap_corruption"></a>バグ チェック 0x13A:KERNEL\_MODE\_HEAP\_CORRUPTION

The KERNEL\_MODE\_HEAP\_CORRUPTION バグ チェックの値は、0x0000013A です。 これは、カーネル モード ヒープ マネージャーがヒープ内で破損を検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルー スクリーン エラー コードが表示される場合は、「[ブルー スクリーン エラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="kernel_mode_heap_corruption-parameters"></a>KERNEL\_MODE\_HEAP\_CORRUPTION のパラメーター

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>検出された破損の種類 (下記の一覧を参照)</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">破損を報告したヒープのアドレス</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">破損が検出されたアドレス</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

### <a name="parameter-1---type-of-heap-corruption"></a>パラメーター 1 - ヒープ破損の種類

0x3: 破損したエントリ ヘッダーが検出されました。

0x4: 複数の破損したエントリ ヘッダーが検出されました。

0x5: 大きな割り当て内で破損したエントリ ヘッダーが検出されました。

0x6: バッファー オーバーランと一致する機能で破損が検出されました。

0x7: バッファー アンダーランと一致する機能で破損が検出されました。

0x8: 空きブロックが、ビジー ブロックにのみ有効な操作に渡されました。

0x9: 現在の操作に対して無効な引数が指定されました。

0xA: 無効な割り当ての種類が検出されました。

0xB: 解放後使用エラーと一致する機能で破損が検出されました。

0xC: 現在の操作に対して不正なヒープが指定されました。

0xD: 破損した空きリストが検出されました。

0xE: ヒープが、空きリスト以外のリストでリストの破損を検出しました。

0xF: 空きブロックが、ビジー ブロックにのみ有効な操作に渡されました。

0x10: 現在の操作中に、ヒープが無効な内部状態を検出しました。 通常、これは、バッファー オーバーフローの結果です。

0x11: 現在の操作中に、ヒープが無効な内部状態を検出しました。 通常、これは、バッファー オーバーフローの結果です。

0x12: 現在の操作中に、ヒープが無効な内部状態を検出しました。 通常、これは、バッファー オーバーフローの結果です。

0x13: ヒープ API が、NULL ヒープ ハンドルに渡されました。 コール スタックを調べて、無効なハンドルがヒープに渡された理由を確認してください。

0x14: 要求されたヒープ割り当てが、現在の割り当て制限を超えています。

0x15: コミット要求の実行中に、要求が現在のコミット制限を超えていると判断されました。

0x16: 指定された VA Manager の割り当てサイズの確認中に、クエリが無効であると判断されました。

## <a name="resolution"></a>解決方法

[ **!analyze**](-analyze.md) デバッグ拡張機能は、バグ チェックに関する情報を表示し、根本原因の特定に役立ちます。

[!heap](-heap.md) 拡張機能は、ヒープ使用量情報の表示、ヒープ マネージャー内のブレークポイントの制御、リークしたヒープ ブロックの検出、ヒープ ブロックの検索、ページ ヒープ情報の表示を行います。
