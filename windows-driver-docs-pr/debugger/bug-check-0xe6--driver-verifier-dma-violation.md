---
title: バグ チェック 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
description: DRIVER_VERIFIER_DMA_VIOLATION のバグ チェックでは、0x000000E6 の値を持ちます。 これは、すべての Driver Verifier DMA の検証違反のバグ チェック コードです。
ms.assetid: badf8948-356c-4728-b34e-02f1638630a6
keywords:
- バグ チェック 0xE6 DRIVER_VERIFIER_DMA_VIOLATION
- DRIVER_VERIFIER_DMA_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DMA_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6835e4d93d2180f6c2ba7dca5a93eb8fce257f83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532265"
---
# <a name="bug-check-0xe6-driververifierdmaviolation"></a>バグ チェック 0xE6 の。ドライバー\_VERIFIER\_DMA\_違反


ドライバー\_VERIFIER\_DMA\_違反のバグ チェックが 0x000000E6 の値を持ちます。 これは、すべての Driver Verifier のバグ チェック コード**DMA の検証**違反。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

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
<td align="left"><p>0x00</p></td>
<td align="left"><p>このコードは、2 つの種類のエラーを表すことができます。</p>
<p>1. ドライバーは、マップの登録ファイルの末尾に過剰なバイトをフラッシュしようとしました。 許可されているバイト数と試行されたバイト数が表示されます。</p>
<p>2. Windows で、連続したマップ レジスタが不足しています。 必要なマップのレジスタの数とマップの連続したレジスタの最大ブロックが表示されます。</p></td>
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
<td align="left"><p>ドライバーには、DMA 共通のバッファーが多すぎますが解放されます。 通常、同じバッファーを 2 回解放に意味します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04</p></td>
<td align="left"><p>ドライバーには、DMA アダプタのチャネルが多すぎますが解放されます。 通常、同じアダプター チャネルを 2 回解放ことを意味します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x05</p></td>
<td align="left"><p>ドライバーが多すぎる DMA のマップのレジスタを解放します。 通常同じマップ レジスタを 2 回解放ことを意味します。 アクティブなマップのレジスタの数が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>ドライバーは、DMA スキャッター/ギャザーのリストが多すぎるを解放します。 通常同じスキャッター/ギャザー リストを 2 回解放ことを意味します。 割り当てられているリストの数と解放の一覧の数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>ドライバーは、最初にそのすべての一般的なバッファーを解放せず、アダプターがリリースしようとしました。 アダプターのアドレスおよび残りのバッファーの数が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>ドライバーは、最初にすべてのアダプターのチャネル、共通のバッファーを解放せず、アダプターをリリースまたはスキャッター/ギャザーのリストを試行します。 アダプターのアドレスおよび残りの項目の数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>ドライバーは、最初にすべてのマップのレジスタを解放せず、アダプターがリリースしようとしました。 アダプターのアドレスと残りのマップのレジスタの数が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>ドライバーは、最初にそのすべてのスキャッター/ギャザー リストを解放せず、アダプターがリリースしようとしました。 アダプターのアドレスおよび残りのスキャッター/ギャザー リストの数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>HV_TOO_MANY_ADAPTER_CHANNELSThe ドライバーには、同時にアダプタのチャネルが多すぎますが割り当てられます。 . (1 つだけのアダプタのチャネルは、アダプターごとに許可されます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>ドライバーは、同時に多くのマップのレジスタを割り当てるしようとしました。 要求された数と許可されている数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>ドライバーは、そのアダプター バッファーをフラッシュできませんでした。 ドライバーをマップしようとしたバイト数とバイト数の最大数が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>ドライバーでは、バッファーをロックすることがなく DMA 転送しようとしました。 問題のバッファーは、ページングされたメモリにしました。 MDL のアドレスが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>割り当てられた、DMA バッファー外ドライバーやハードウェアを作成しました。 (オーバーランまたはアンダーラン) エラーの性質と、関連するアドレスが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10</p></td>
<td align="left"><p>そのマップを解放しようとしています。 ドライバーは、いくつかまだマップされているときに登録します。 マップのレジスタに割り当てられた状態の数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x11</p></td>
<td align="left"><p>ドライバーは、アダプターの未解決の参照カウントが多すぎます。 参照カウントとアダプターのアドレスの数が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x13</p></td>
<td align="left"><p>ドライバーでは、不適切な IRQL で DMA ルーチンが呼び出されます。 必要な IRQL と実際の IRQL が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x14</p></td>
<td align="left"><p>ドライバーでは、不適切な IRQL で DMA ルーチンが呼び出されます。 必要な IRQL と実際の IRQL が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x15</p></td>
<td align="left"><p>ドライバーは、多くのマップのレジスタを割り当てるしようとしました。 要求された数と許可されている数が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x16</p></td>
<td align="left"><p>ドライバーは、マップされていないバッファーをフラッシュしようとしました。 バッファーのアドレスが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x18</p></td>
<td align="left"><p>ドライバーでは、既にリリースされ、存在しないアダプターを使用して、DMA 操作をしようとしました。 アダプターのアドレスが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x19</p></td>
<td align="left"><p>ドライバーでは、HAL ルーチンに null DMA_ADAPTER 値が渡されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1B</p></td>
<td align="left"><p>ドライバーには、HAL のルーチンへのアドレスおよび MDL が渡されます。 ただし、このアドレスにはこの MDL の境界内でありません。 アドレスが渡され、MDL のアドレスが表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1D</p></td>
<td align="left"><p>ドライバーが既にマップされていますが、アドレス範囲をマップしようとしました。 アドレス範囲とその範囲の現在のマッピングが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1E</p></td>
<td align="left"><p>ドライバーと呼ばれる<strong>HalGetAdapter</strong>します。 この関数は廃止されています--使用する必要があります<strong>IoGetDmaAdapter</strong>代わりにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1F</p></td>
<td align="left"><p>HV_BAD_MDLThe ドライバーには、無効なシステム アドレス - 最初の MDL 前に、または後の最初の MDL または MDL バッファーよりも長いし、MDL 内のページ境界を越える転送の長さを使用してエンドが参照されています。 . 無効なアドレスと最初の MDL アドレスまたは MDL アドレスと転送の余分な長さが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x20</p></td>
<td align="left"><p>マップをフラッシュしようとしています。 ドライバーの登録を&#39;t されたマップ。 マップの登録ベース、フラッシュのアドレス MDL が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x21</p></td>
<td align="left"><p>ドライバーが長さ 0 のバッファー転送をマップしようとしました。</p></td>
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

Driver Verifier **DMA の検証**オプションは、Windows XP およびそれ以降のバージョンで使用できるのみです。 詳細については、Driver Verifier は、Windows ドライバー キットを参照してください。

 

 




