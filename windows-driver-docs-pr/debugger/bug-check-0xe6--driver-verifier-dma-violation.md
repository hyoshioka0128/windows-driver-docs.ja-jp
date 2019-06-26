---
title: バグ チェック 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
description: DRIVER_VERIFIER_DMA_VIOLATION のバグ チェックでは、0x000000E6 の値を持ちます。 これは、すべての Driver Verifier DMA の検証違反のバグ チェック コードです。
ms.assetid: badf8948-356c-4728-b34e-02f1638630a6
keywords:
- バグ チェック 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
- DRIVER_VERIFIER_DMA_VIOLATION
ms.date: 05/07/2019
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DMA_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: deac160416738fceba842b4cd880d0e20d68233e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367111"
---
# <a name="bug-check-0xe6-driververifierdmaviolation"></a>バグ チェック 0xE6:ドライバー\_VERIFIER\_DMA\_違反


ドライバー\_VERIFIER\_DMA\_違反のバグ チェックが 0x000000E6 の値を持ちます。 これは、すべての Driver Verifier のバグ チェック コード**DMA の検証**違反。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="driververifierdmaviolation-parameters"></a>ドライバー\_VERIFIER\_DMA\_違反パラメーター


パラメーター 1 は、関心のある唯一のパラメーターです。 このパラメーターは、正確な違反を識別します。 デバッガーがアタッチされている場合は、デバッガーで情報メッセージが表示されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">エラーの原因とデバッガーのメッセージ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00 - その他の DMA エラー。</p></td>
<td align="left"><p>このコードは、2 番目のパラメーターで示されている 2 つの種類のエラーを表すことができます。</p>
<p>0x1 - ドライバーは、マップ登録ファイルの末尾に過剰なバイトをフラッシュしようとしました。 
<p>MDL の残りの 3 番目のバイト数のパラメーター。</p>
<p>パラメーター 4 - をフラッシュする要求の残りのバイト数。</p>
<p>0x2 - Windows が連続したマップ レジスタから実行します。 </p>
<p>パラメーター 3 - マップのレジスタが必要です。</p>
<p>パラメーター 4 - 連続したマップの数を登録します。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p></td>
<td align="left"><p>パフォーマンス カウンターが減少しています。 カウンターの新旧の値が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x02</p></td>
<td align="left"><p>パフォーマンス カウンターが急速に増加しています。 このカウンターの値は、デバッガーに表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x03</p></td>
<td align="left"><p>ドライバーには、DMA 共通のバッファーが多すぎますが解放されます。 通常、同じバッファーを 2 回解放に意味します。 </p>
<p>2 - 数のパラメーターの一般的な余分なバッファーを解放します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>ドライバーには、DMA アダプタのチャネルが多すぎますが解放されます。 通常、同じアダプター チャネルを 2 回解放ことを意味します。</p>
<p> 2 - パラメーター解放余分なアダプターのチャネルの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>ドライバーが多すぎる DMA のマップのレジスタを解放します。 通常同じマップ レジスタを 2 回解放ことを意味します。 </p>
<p>2 - パラメーター解放マップの追加のレジスタの数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>ドライバーは、DMA スキャッター/ギャザーのリストが多すぎるを解放します。 通常同じスキャッター/ギャザー リストを 2 回解放ことを意味します。</p>
<p>パラメーター 2 - 割り当てられたスキャッター/ギャザーが一覧表示します。 </p>
<p>パラメーター 3 - 解放スキャッター/ギャザーが一覧表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>ドライバーは、最初にそのすべての一般的なバッファーを解放せず、アダプターがリリースしようとしました。 </p>
<p> パラメーター 2 - DMA アダプターへのポインター。</p>
<p> パラメーター 3 - 一般的な未処理のバッファーの数。</p>
<p> パラメーター 4 - 対応する内部の検証データへのポインター。 </p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>ドライバーは、最初にすべてのアダプターのチャネル、共通のバッファーを解放せず、アダプターをリリースまたはスキャッター/ギャザーのリストを試行します。 <p> <p> パラメーター 2 - DMA アダプターへのポインター。
<p> パラメーター 3 - 未処理のアダプタのチャネルの数。
<p> パラメーター 4 - 対応する内部の検証データへのポインター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>ドライバーは、最初にすべてのマップのレジスタを解放せず、アダプターがリリースしようとしました。</p> 
<p>パラメーター 2 - DMA アダプターへのポインター。</p>
<p>パラメーター 3 - 未処理のマップの数を登録します。</p>
<p>パラメーター 4 - 対応する内部の検証データへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>ドライバーは、最初にそのすべてのスキャッター/ギャザー リストを解放せず、アダプターがリリースしようとしました。 </p>
<p>パラメーター 2 - DMA アダプターへのポインター。</p>
<p>パラメーター 3 - 未処理のスキャッター/ギャザーの数が一覧表示します。</p>
<p>パラメーター 4 - 対応する内部の検証データへのポインター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>ドライバーによってアダプターのチャネルが多すぎますが (1 つだけのアダプタのチャネルは、アダプターごとに許可されます)。 同時に割り当て</p>
<p>パラメーター 2 - 未処理のアダプタのチャネル。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ドライバーは、同時に多くのマップのレジスタを割り当てるしようとしました。 </p>
<p>パラメーター 2 - 必要なマップを登録します。</p>
<p>パラメーター 3 - 最大マップに登録します。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ドライバーは、そのアダプター バッファーをフラッシュできませんでした。</p>
<p>マップ パラメーター 2 - バイト数。</p>
<p>3 - パラメーターを時にマップできるバイトの最大数。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>ドライバーでは、バッファーをロックすることがなく DMA 転送しようとしました。 問題のバッファーは、ページングされたメモリにしました。 </p>
<p>パラメーター 2 - DMA のアドレスの MDL をバッファーします。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>割り当てられた、DMA バッファー外ドライバーやハードウェアを作成しました。 2 番目のパラメーターは、違反コードを示します。</p>

<p>0x01 :前に、DMA バッファーが変更されたタグ。想定されるタグは、DmaVrfy0 です。</p>
<p>3 - バッファーの長さのパラメーター。</p>
<p>パラメーター 4 - バッファーを起動します。</p>
<p>0x02 :DMA バッファーが変更された後のタグ。</p>
想定されるタグは、DmaVrfy0 です。
<p>3 - バッファーの長さのパラメーター。</p>
<p>パラメーター 4 - バッファーを起動します。</p>
0x03 :無料のマップのレジスタが上書きされました。</p>
<p>パラメーター 3 - 破損アドレス。 予想される塗りつぶしのパターンでは、0x0F です。</p>
0x04 :バッファーが誤って変更された前に、のスペースです。</p>
<p>パラメーター 3 - バッファーを起動します。 必要な埋め込みは、0x0F です。</p>
<p>パラメーター 4 - 破損アドレス。</p>
0x05 :バッファーが誤って変更された後のスペースです。</p>
<p>パラメーター 3 - バッファーを起動します。</p>
<p>パラメーター 4 - 破損アドレス。 予想される埋め込みパターンでは、0x0F です。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>そのマップを解放しようとしています。 ドライバーは、いくつかまだマップされているときに登録します。 </p>
<p>まだマップされているレジスタの 2 - 数のパラメーター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>ドライバーは、アダプターの未解決の参照カウントが多すぎます。 </p>
<p>2 番目の参照カウントのパラメーター。</p>
<p>パラメーター 3 - DMA アダプターへのポインター。</p>
<p>パラメーター 4 - 対応する内部の検証データへのポインター。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>ドライバーでは、不適切な IRQL で DMA ルーチンが呼び出されます。 2 番目のパラメーターは、違反コードを示します。</p>
0x01 :現在の IRQL が予想と異なります。
<p>3 - 必要な IRQL のパラメーター。</p>
<p>4 - 現在の IRQL のパラメーター。</p>
0x02 :現在の IRQL が予想よりも大きいです。</p>
<p>パラメーター 3 - には、最大の IRQL が必要です。</p>
<p>4 - 現在の IRQL のパラメーター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ドライバーでは、不適切な IRQL で DMA ルーチンが呼び出されます。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ドライバーは、多くのマップのレジスタを割り当てるしようとしました。</p> 
<p>パラメーター 2 に割り当てられているマップを登録します。</p>
<p>パラメーター 3 - 最大マップに登録します。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>ドライバーは、マップされていないバッファーをフラッシュしようとしました。 </p>
<p>パラメーター 2 - マップのシステムの仮想空間内のアドレスを登録します。</p>
<p>パラメーター 3 に対応する内部の検証データへのポインター。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>ドライバーでは、既にリリースされ、存在しないアダプターを使用して、DMA 操作をしようとしました。 </p>
<p>パラメーター 2 - DMA アダプターへのポインター。</p>
<p>パラメーター 3 に対応する内部の検証データへのポインター。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>ドライバーでは、HAL ルーチンに null DMA_ADAPTER 値が渡されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>ドライバーには、HAL のルーチンへのアドレスおよび MDL が渡されます。 ただし、このアドレスにはこの MDL の境界内でありません。 </p>
<p>パラメーター 2 - 仮想アドレスが MDL の範囲外です。</p>
<p>パラメーター 3 - MDL です。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>ドライバーが既にマップされていますが、アドレス範囲をマップしようとしました。 </p>
<p>パラメーター 2 の開始をマップするバッファー。 </p>
<p>パラメーター 3 には、マップの末尾にバッファーします。 </p>
<p>4 - システム アドレスは既にマップされているバッファー内のパラメーター。
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>ドライバーと呼ばれる<strong>HalGetAdapter</strong>します。 この関数は廃止されています--使用する必要があります<strong>IoGetDmaAdapter</strong>代わりにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p> DMA バッファーが無効です。 ドライバーには、無効なシステム アドレス - 最初の MDL 前に、または後の最初の MDL または MDL バッファーよりも長いし、MDL 内のページ境界を越える転送の長さを使用してエンドが参照されています。2 番目のパラメーターは、違反コードを示します。</p>
<p>0x01 :仮想バッファーのアドレスは、最初の MDL 前に、です。</p>
<p>パラメーター 3 - DMA バッファーの先頭の仮想アドレス。</p>
<p>4 - パラメーター DMA バッファーを記述する最初の MDL へのポインター。</p>

<p>0x02 :仮想アドレスは、後の最初の MDL です。</p>
<p>パラメーター 3 - DMA バッファーの先頭の仮想アドレス。</p>
<p>4 - パラメーター DMA バッファーを記述する最初の MDL へのポインター。</p>

<p>0x03 :余分な転送の長さは、ページの境界を越えます。</p>
<p>パラメーター 3 - DMA バッファーを記述する MDL へのポインター。</p>
<p>パラメーター 4 - DMA の長さを転送します。

<p>0x04 :DMA バッファーの仮想のアドレスは、キャッシュの配置ではありません。
<p>パラメーター 3 - DMA バッファーの先頭の仮想アドレス。</p>
<p>パラメーター 4 - DMA バッファーを記述する MDL へのポインター。</p>

<p>0x05 :DMA バッファーの長さは、キャッシュの配置ではありません。</p>
<p>3 - DMA バッファーの長さのパラメーター。</p>
<p>パラメーター 4 - DMA バッファーを記述する MDL へのポインター。
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>ドライバーは、マップされていない map レジスタをフラッシュしようとしました。</p>
<p>パラメーター 2 - マップには、ベースを登録します。</p>
<p>パラメーター 3 - DMA バッファーの先頭の VA です。</p>
<p>パラメーター 4 - MDL へのポインターは、DMA バッファーの記述に使用されます。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>ドライバーが長さ 0 のバッファー転送をマップしようとしました。</p>
<p>パラメーター 2 に対応する内部の検証データへのポインター。</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>0x22</p></td>
<td align="left"><p>DMA バッファーの問い合わせください。 システムにマップされていません</p>
<p>パラメーター 2 - MDL</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x23</p></td>
<td align="left"><p>完了するかキャンセルされていないチャネルをフラッシュできません。 </p>
<p>パラメーター 2 - 違反コード。 </p>
<p>値:0x00:無効なチャネルのフラッシュ </p>
<p>パラメーター 3 - コント ローラーの id。</p>
<p>パラメーター 4 - チャネルの数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x24</p></td>
<td align="left"><p>要求された長さのバッファーが不足します。</p>
<p>2 - 原因不明の長さのパラメーター。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x25</p></td>
<td align="left"><p>不明なデバイスの説明のバージョンです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x26</p></td>
<td align="left"><p>IOMMU は DMA の違反を検出しました。 </p>
<p>2 - 障害が発生してデバイスのデバイス オブジェクトのパラメーター。</p>
<p>パラメーター 3 - エラー発生の情報 (通常の障害発生の物理アドレス)。</p>
<p>パラメーター 4 - エラーの種類 (ハードウェアの特定) します。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

原因の詳細については、パラメーター セクション内の各コードの説明を参照してください。

<a name="resolution"></a>解決方法
----------

このバグ チェックは、Driver Verifier が 1 つまたは複数のドライバーを監視するように指示された場合にのみ発生します。 Driver Verifier の使用は意図しない、非アクティブ化する必要があります。 この問題の原因となったドライバーを削除しても検討する可能性があります。

ドライバー開発者の場合は、このバグ チェックで得られた情報を使用して、コードで、バグを修正します。

Driver Verifier の詳細については、次を参照してください。 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。

 

 




