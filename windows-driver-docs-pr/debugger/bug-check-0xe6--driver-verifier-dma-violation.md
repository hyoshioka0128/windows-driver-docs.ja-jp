---
title: バグチェック 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
description: DRIVER_VERIFIER_DMA_VIOLATION バグチェックの値は0x000000E6 です。 これは、すべての Driver Verifier DMA 検証違反のバグチェックコードです。
ms.assetid: badf8948-356c-4728-b34e-02f1638630a6
keywords:
- バグチェック 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
- DRIVER_VERIFIER_DMA_VIOLATION
ms.date: 05/07/2019
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DMA_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d94e775611b7b0e1baf0726954c9f6906caeb441
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402277"
---
# <a name="bug-check-0xe6-driver_verifier_dma_violation"></a>バグチェック 0xE6: ドライバーの検証機能の \_ \_ DMA \_ 違反


DRIVER \_ VERIFIER \_ DMA 違反のバグチェックには、 \_ 値として0x000000e6 が指定されています。 これは、すべての Driver Verifier **DMA 検証**違反のバグチェックコードです。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

> [!NOTE]
> ドライバーの検証ツールが有効になっていない場合は、E6 主要なバグチェックコードを確認できます。 ドライバーの検証ツールが有効になっていない状態でこのコードが発生する場合は、 [DMA の検証](https://docs.microsoft.com/windows-hardware/drivers/devtest/dma-verification)に関するページを参照してください。 

## <a name="driver_verifier_dma_violation-parameters"></a>ドライバーの \_ 検証ツールの \_ DMA \_ 違反パラメーター


パラメーター1が対象の唯一のパラメーターです。 このパラメーターは、厳密な違反を識別します。 デバッガーがアタッチされている場合は、情報メッセージがデバッガーに表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">エラーとデバッガーのメッセージの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00-その他の DMA エラー。</p></td>
<td align="left"><p>このコードは、パラメーター2で示されているように、2種類のエラーを表すことができます。</p>
<p>0x1-ドライバーは、マップレジスタファイルの末尾にバイトをフラッシュしようとしました。 
<p>パラメーター 3-MDL に残されているバイト数。</p>
<p>パラメーター 4-フラッシュが要求された残りのバイト数。</p>
<p>0x2-Windows が連続したマップレジスタを使い果たしました。 </p>
<p>パラメーター 3-マップレジスタが必要です。</p>
<p>パラメーター 4-連続するマップレジスタの数。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>パフォーマンスカウンターが低下しました。 カウンターの古い値と新しい値が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>パフォーマンスカウンターが急激に増加しています。 カウンター値がデバッガーに表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>ドライバーにより、DMA 共通バッファーが過剰に解放されています。 通常、これは、同じバッファーを2回解放することを意味します。 </p>
<p>パラメーター 2-余分な共通バッファーが解放された回数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>ドライバーにより、DMA アダプターチャネルが過剰に解放されています。 通常、これは同じアダプターチャネルを2回解放することを意味します。</p>
<p> パラメーター 2-余分なアダプターチャネルが解放された回数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>ドライバーにより、DMA マップレジスタが過剰に解放されています。 通常、これは、同じマップレジスタが2回解放されたことを意味します。 </p>
<p>パラメーター 2-追加のマップレジスタが解放された回数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>ドライバーによって、DMA のスキャッター/ギャザーリストが過剰に解放されています。 通常、これは、同じスキャッター/ギャザーリストを2回解放したことを意味します。</p>
<p>パラメーター 2-割り当てられたスキャッター/ギャザーリスト。 </p>
<p>パラメーター 3-解放されたスキャッター/ギャザーリスト。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>ドライバーは、最初にすべての共通バッファーを解放せずにアダプターを解放しようとしました。 </p>
<p> パラメーター 2-DMA アダプターへのポインター。</p>
<p> パラメーター 3-未処理の共通バッファーの数。</p>
<p> パラメーター 4-対応する内部検証データへのポインター。 </p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>ドライバーは、最初にすべてのアダプターチャネル、共通バッファー、またはスキャッター/ギャザーリストを解放せずにアダプターを解放しようとしました。 <p> <p> パラメーター 2-DMA アダプターへのポインター。
<p> パラメーター 3-未処理のアダプターチャネルの数。
<p> パラメーター 4-対応する内部検証データへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>ドライバーは、最初にすべてのマップレジスタを解放せずにアダプターを解放しようとしました。</p> 
<p>パラメーター 2-DMA アダプターへのポインター。</p>
<p>パラメーター 3-未処理のマップレジスタの数。</p>
<p>パラメーター 4-対応する内部検証データへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>ドライバーは、最初にすべてのスキャッター/ギャザーリストを解放せずにアダプターを解放しようとしました。 </p>
<p>パラメーター 2-DMA アダプターへのポインター。</p>
<p>パラメーター 3-未処理のスキャッター/ギャザーリストの数。</p>
<p>パラメーター 4-対応する内部検証データへのポインター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>ドライバーで割り当てられているアダプターチャネルが多すぎます (アダプターごとに1つのアダプターチャネルのみが許可されます)。</p>
<p>パラメーター 2-未処理のアダプターチャネル。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ドライバーが割り当てられているマップレジスタの数が多すぎます。 </p>
<p>パラメーター 2-必須のマップレジスタ。</p>
<p>パラメーター 3-マップの最大レジスタ。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ドライバーは、アダプターバッファーをフラッシュしませんでした。</p>
<p>パラメーター 2-マップされたバイト数。</p>
<p>パラメーター 3-一度にマップできる最大バイト数。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>ドライバーは、バッファーをロックせずに DMA 転送を試行しました。 問題のバッファーがページメモリにありました。 </p>
<p>パラメーター 2-DMA バッファー MDL のアドレス。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>ドライバーまたはハードウェアが、割り当てられた DMA バッファーの外部に書き込まれました。 パラメーター2は違反コードです。</p>

<p>0x01: DMA バッファーが変更される前のタグ。必要なタグは DmaVrfy0 です。</p>
<p>パラメーター 3-バッファーの長さ。</p>
<p>パラメーター 4-バッファーを開始します。</p>
<p>0x02: DMA バッファーが変更された後のタグ。</p>
必要なタグは DmaVrfy0 です。
<p>パラメーター 3-バッファーの長さ。</p>
<p>パラメーター 4-バッファーを開始します。</p>
0x03: Free マップレジスタが上書きされました。</p>
<p>パラメーター 3-破損アドレス。 必要な fill pattern は0x0F です。</p>
0x04: バッファーが誤って変更される前の埋め込み。</p>
<p>パラメーター 3-バッファーを開始します。 必要な埋め込みは0x0F です。</p>
<p>パラメーター 4-破損アドレス。</p>
0x05: バッファーが誤って変更された後の埋め込み。</p>
<p>パラメーター 3-バッファーを開始します。</p>
<p>パラメーター 4-破損アドレス。 必要な埋め込みパターンは0x0F です。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>ドライバーはマップレジスタを解放しようとしましたが、まだマップされていませんでした。 </p>
<p>パラメーター 2-まだマップされているレジスタの数。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>ドライバーに、アダプターの未解決の参照カウントが多すぎます。 </p>
<p>パラメーター 2-参照カウント。</p>
<p>パラメーター 3-DMA アダプターへのポインター。</p>
<p>パラメーター 4-対応する内部検証データへのポインター。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>ドライバーは、正しくない IRQL で DMA ルーチンを呼び出しました。 パラメーター2は違反コードです。</p>
0x01: 現在の IRQL が予期されたものと異なります。
<p>パラメーター 3-必要な IRQL。</p>
<p>パラメーター 4-現在の IRQL。</p>
0x02: 現在の IRQL が予想よりも高くなっています。</p>
<p>パラメーター 3-最大 IRQL が必要です。</p>
<p>パラメーター 4-現在の IRQL。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ドライバーは、正しくない IRQL で DMA ルーチンを呼び出しました。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ドライバーが割り当てられているマップレジスタの数が多すぎます。</p> 
<p>パラメーター 2-割り当てられたマップレジスタ。</p>
<p>パラメーター 3-マップの最大レジスタ。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>ドライバーは、マップされていないバッファーをフラッシュしようとしました。 </p>
<p>パラメーター 2-マップレジスタのシステム仮想空間内のアドレス。</p>
<p>パラメーター 3-対応する内部検証データへのポインター。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>ドライバーは既に解放され、存在しないアダプターを使用して、DMA 操作を試行しました。 </p>
<p>パラメーター 2-DMA アダプターへのポインター。</p>
<p>パラメーター 3-対応する内部検証データへのポインター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>ドライバーにより、HAL ルーチンに null DMA_ADAPTER 値が渡されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>ドライバーは、アドレスと MDL を HAL ルーチンに渡しました。 ただし、このアドレスはこの MDL の境界内にありません。 </p>
<p>パラメーター 2-MDL の境界外の仮想アドレス。</p>
<p>パラメーター 3-MDL。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>ドライバーは、既にマップされているアドレス範囲をマップしようとしました。 </p>
<p>パラメーター 2-マップを開始するためのバッファー。 </p>
<p>パラメーター 3-map end へのバッファー。 </p>
<p>パラメーター 4-既にマップされているバッファー内のシステムアドレス。
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>ドライバーは<strong>HalGetAdapter</strong>を呼び出しました。 この関数は互換性のために残されています。代わりに<strong>IoGetDmaAdapter</strong>を使用する必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p> DMA バッファーが無効です。 ドライバーは、最初の MDL の前、または最初の MDL の後、または MDL バッファーより長く、mdl 内のページ境界を越える転送長を使用して、無効なシステムアドレスを参照しました。パラメーター2は違反コードです。</p>
<p>0x01: 最初の MDL より前の仮想バッファーアドレスです。</p>
<p>パラメーター 3-DMA バッファーの開始の仮想アドレス。</p>
<p>パラメーター 4-DMA バッファーを記述する最初の MDL へのポインター。</p>

<p>0x02: 仮想アドレスが最初の MDL の後にあります。</p>
<p>パラメーター 3-DMA バッファーの開始の仮想アドレス。</p>
<p>パラメーター 4-DMA バッファーを記述する最初の MDL へのポインター。</p>

<p>0x03: 余分な転送の長さがページの境界を超えています。</p>
<p>パラメーター 3-DMA バッファーを記述する MDL へのポインター。</p>
<p>パラメーター 4-DMA 転送の長さ。

<p>0x04: DMA バッファーの仮想アドレスがキャッシュに固定されていません。
<p>パラメーター 3-DMA バッファーの開始の仮想アドレス。</p>
<p>パラメーター 4-DMA バッファーを記述する MDL へのポインター。</p>

<p>0x05: DMA バッファーの長さがキャッシュに固定されていません。</p>
<p>パラメーター 3-DMA バッファーの長さ。</p>
<p>パラメーター 4-DMA バッファーを記述する MDL へのポインター。
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>ドライバーは、マップされていないマップレジスタをフラッシュしようとしました。</p>
<p>パラメーター 2-Map レジスタ base。</p>
<p>パラメーター 3-DMA バッファーの開始の VA。</p>
<p>パラメーター 4-DMA バッファーの記述に使用される MDL へのポインター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>ドライバーは、転送用に長さ0のバッファーをマップしようとしました。</p>
<p>パラメーター 2-対応する内部検証データへのポインター。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>DMA バッファーがシステム VA でマップされていません。</p>
<p>パラメーター 2-MDL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>完了していないチャネルまたは取り消されたチャネルをフラッシュすることはできません。 </p>
<p>パラメーター 2-違反コード。 </p>
<p>値: 0x00: 無効なチャネルフラッシュ </p>
<p>パラメーター 3-コントローラー Id。</p>
<p>パラメーター 4-チャネル番号。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>要求された長さのバッファーが不足しています。</p>
<p>パラメーター 2-Unaccounted の長さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>不明なデバイスの説明のバージョンです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>IOMMU で DMA 違反が検出されました。 </p>
<p>パラメーター 2-エラーが発生しているデバイスのデバイスオブジェクト。</p>
<p>パラメーター 3-エラーが発生している情報 (通常は、障害が発生した物理アドレス)。</p>
<p>パラメーター 4-エラーの種類 (ハードウェア固有)。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

原因の説明については、「Parameters」セクションの各コードの説明を参照してください。

<a name="resolution"></a>解決方法
----------

このバグチェックは、ドライバーの検証ツールで1つ以上のドライバーを監視するように指示されている場合にのみ発生します。 ドライバーの検証ツールを使用しない場合は、非アクティブ化する必要があります。 また、この問題の原因となったドライバーを削除することも考えられます。

ドライバーライターの場合は、このバグチェックで取得した情報を使用して、コード内のバグを修正します。

ドライバーの検証機能の詳細については、「 [Driver verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

 

 




