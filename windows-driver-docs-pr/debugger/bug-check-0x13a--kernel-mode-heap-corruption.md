---
title: バグチェック 0x13A KERNEL_MODE_HEAP_CORRUPTION
description: KERNEL_MODE_HEAP_CORRUPTION のバグチェックの値は0x0000013A です。 これは、カーネルモードヒープマネージャーがヒープ内の破損を検出したことを示します。
ms.assetid: 806669B3-B811-462A-A3B6-2F583BF0E19A
keywords:
- バグチェック 0x13A KERNEL_MODE_HEAP_CORRUPTION
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
# <a name="bug-check-0x13a-kernel_mode_heap_corruption"></a>バグチェック 0x13A: カーネル\_モード\_ヒープ\_破損

カーネル\_モード\_ヒープ\_破損バグチェックには、0x0000013A という値が指定されています。 これは、カーネルモードヒープマネージャーがヒープ内の破損を検出したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="kernel_mode_heap_corruption-parameters"></a>カーネル\_モード\_ヒープ\_破損パラメーター

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
<td align="left"><p>検出された破損の種類-下の一覧を参照</p></td>
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

### <a name="parameter-1---type-of-heap-corruption"></a>パラメーター 1-ヒープ破損の種類

0x3: 破損したエントリヘッダーが検出されました。

0x4: 複数の破損したエントリヘッダーが検出されました。

0x5: 大きな割り当てで破損したエントリヘッダーが検出されました。

0x6: バッファーオーバーランと一貫性のある機能があるため、破損が検出されました。

0x7: バッファーアンダーランと一貫性のある機能があるため、破損が検出されました。

0x8: 空きブロックが、ビジー状態のブロックに対してのみ有効な操作に渡されました。

0x9: 現在の操作に無効な引数が指定されました。

0xA: 無効な割り当ての種類が検出されました。

0xB: 機能が使用できないエラーと一致する機能があるため、破損が検出されました。

0xC: 現在の操作に対して間違ったヒープが指定されました。

0xD: 破損したフリーリストが検出されました。

0xE: ヒープが、リスト内の空きリスト以外の破損を検出しました。

0Xf です: 空きブロックが、ビジー状態のブロックに対してのみ有効な操作に渡されました。

0x10: 現在の操作中に、ヒープによって無効な内部状態が検出されました。 通常、これはバッファーオーバーフローの結果です。

0x11: 現在の操作中に、ヒープによって無効な内部状態が検出されました。 通常、これはバッファーオーバーフローの結果です。

0x12: 現在の操作中に、ヒープによって無効な内部状態が検出されました。 通常、これはバッファーオーバーフローの結果です。

0x13: ヒープ API に NULL ヒープハンドルが渡されました。 呼び出し履歴を確認し、無効なハンドルがヒープに渡された理由を判断します。

0x14: 要求されたヒープ割り当てが、現在の割り当て制限を超えています。

0x15: コミット要求を実行するプロセスでは、要求が現在のコミット制限を超えていると判断されました。

0x16: 指定された VA マネージャー割り当てのサイズを確認するプロセスで、クエリが無効であると判断されました。

## <a name="resolution"></a>解決方法

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

[! Heap](-heap.md)拡張機能では、ヒープ使用量の情報の表示、ヒープマネージャーでのブレークポイントの制御、リークしたヒープブロックの検出、ヒープブロックの検索、またはページヒープ情報の表示を行います。
