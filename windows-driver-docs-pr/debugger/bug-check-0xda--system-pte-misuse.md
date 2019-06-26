---
title: バグ チェック 0 xda SYSTEM_PTE_MISUSE
description: SYSTEM_PTE_MISUSE のバグ チェックでは、0x000000DA の値を持ちます。 これは、不適切な方法でページ テーブル エントリ (PTE) ルーチンが使用されたことを示します。
ms.assetid: a9a9f3e9-39b7-4e4a-a326-2f510e0aaa99
keywords:
- バグ チェック 0 xda SYSTEM_PTE_MISUSE
- SYSTEM_PTE_MISUSE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_PTE_MISUSE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d15af41c4b11739b5e03bff1718b639071b3fd8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367130"
---
# <a name="bug-check-0xda-systemptemisuse"></a>バグ チェック 0xDA:システム\_PTE\_誤用


システム\_PTE\_誤用のバグ チェックが 0x000000DA の値を持ちます。 これは、不適切な方法でページ テーブル エントリ (PTE) ルーチンが使用されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="systemptemisuse-parameters"></a>システム\_PTE\_誤用パラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

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
<td align="left"><p>0x01</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>メモリの記述子のリストのアドレス</p></td>
<td align="left"><p>構造体を追跡する内部ロックに重複するアドレス</p></td>
<td align="left"><p>解放されるマッピングは、重複しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>解放するため、システムが必要とするマッピングの数</p></td>
<td align="left"><p>解放するため、ドライバーが要求しているマッピングの数</p></td>
<td align="left"><p>解放されているマッピングの数が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>見つかった最初の追跡の内部構造体のアドレス</p></td>
<td align="left"><p>マッピングのアドレスを解放する、システムが必要とします。</p></td>
<td align="left"><p>マッピングのアドレスを解放するドライバーが要求しています。</p></td>
<td align="left"><p>解放されているマッピングのアドレスが正しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>構造体を追跡する内部ロックのアドレス</p></td>
<td align="left"><p>MDL で最初にページ フレーム番号、システムが必要とする必要があります。</p></td>
<td align="left"><p>MDL で最初に現在あるページ フレームの数</p></td>
<td align="left"><p>MDL がマップされるため、マップされた MDL の最初のページが変更されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>見つかった最初の追跡の内部構造体のアドレス</p></td>
<td align="left"><p>仮想アドレスを解放する、システムが必要とします。</p></td>
<td align="left"><p>解放するため、ドライバーが要求している仮想アドレス</p></td>
<td align="left"><p>MDL がマップされるため、解放される MDL で開始仮想アドレスが変更されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>ドライバーで指定された MDL</p></td>
<td align="left"><p>ドライバーによって指定された仮想アドレス</p></td>
<td align="left"><p>無料へのマッピングの数 (ドライバーで指定)</p></td>
<td align="left"><p>解放される MDL ことがない (または現在はできません) マップします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>初期のマッピング</p></td>
<td align="left"><p>マッピングの数</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>(Windows 2000 のみ)マッピング範囲は、double 型に割り当てられたことです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>初期のマッピング</p></td>
<td align="left"><p>呼び出し元が解放するマッピングの数</p></td>
<td align="left"><p>システムと思われるマッピングの数を解放する必要があります。</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元は無料のマッピングの数が不適切に要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>初期のマッピング</p></td>
<td align="left"><p>呼び出し元が解放されるマッピングの数</p></td>
<td align="left"><p>システムとしているマッピング インデックスに空きが既に</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元がいくつかのマッピングを解放するよう求めるが、うち少なくとも 1 つは割り当てられていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p><strong>1:</strong>ドライバーは、MDL で「エラー発生時のバグ チェック」を要求します。</p>
<p><strong>0:</strong>ドライバーは、MDL で「エラー発生時のバグ チェック」を要求していません。</p></td>
<td align="left"><p>呼び出し元が割り当てるマッピングの数</p></td>
<td align="left"><p>要求したマッピング共有の種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が 0 のマッピングを割り当てること確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>破損しているマッピング</p></td>
<td align="left"><p>呼び出し元が割り当てるマッピングの数</p></td>
<td align="left"><p>要求したマッピング共有の種類</p></td>
<td align="left"><p>(Windows 2000 のみ)マッピングのリストが既にこの割り当て時に壊れています。 破損しているマッピングは、最下位の可能なマッピングのアドレスの下にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>破損しているマッピング</p></td>
<td align="left"><p>呼び出し元が割り当てるマッピングの数</p></td>
<td align="left"><p>要求したマッピング共有の種類</p></td>
<td align="left"><p>(Windows 2000 のみ)マッピングのリストが既にこの割り当て時に壊れています。 破損しているマッピングは、最下位の可能なマッピング アドレス上にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>初期のマッピング</p></td>
<td align="left"><p>呼び出し元が解放されるマッピングの数</p></td>
<td align="left"><p>プールのマッピングの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が 0 のマッピングを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>初期のマッピング</p></td>
<td align="left"><p>呼び出し元が解放されるマッピングの数</p></td>
<td align="left"><p>プールのマッピングの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)マッピングを解放しようとして、呼び出し元が guard のマッピングが上書きされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>存在しないマッピング</p></td>
<td align="left"><p>呼び出し元が解放しようとするマッピングの数</p></td>
<td align="left"><p>解放されているマッピング共有の種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が存在しないマッピングを解放しようとしています。 存在しないマッピングは、最下位の可能なマッピングのアドレスの下にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>存在しないマッピング</p></td>
<td align="left"><p>呼び出し元が解放しようマッピングの数</p></td>
<td align="left"><p>解放されているマッピング共有の種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が存在しないマッピングを解放しようとしています。 存在しないマッピングは、最上位の可能なマッピング アドレス上にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>存在しないマッピング</p></td>
<td align="left"><p>呼び出し元が解放しようとするマッピングの数</p></td>
<td align="left"><p>解放されているマッピング共有の種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が存在しないマッピングを解放しようとしています。 存在しないマッピングでは、マッピングのアドレス空間のベースに位置します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>要求されているマッピングの数</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>このルーチンの呼び出し元が呼び出されるルーチンのアドレス</p></td>
<td align="left"><p> 呼び出し元は、0 のマッピングを要求します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>所有者の識別タグ</p></td>
<td align="left"><p> 呼び出し元が所有していないマッピング アドレス範囲を解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>マッピングのアドレス空間を解放しようとして、呼び出し元では、一見空です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x103</p></td>
<td align="left"><p>無効なマッピングのアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>マッピングのアドレス空間内のマッピングの数</p></td>
<td align="left"><p>マッピングのアドレス空間を解放しようとして、呼び出し元は、まだ予約されています。 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapreservedmapping" data-raw-source="[MmUnmapReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapreservedmapping)">MmUnmapReservedMapping</a></strong></p>
<p>前に呼び出す必要があります <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreemappingaddress" data-raw-source="[MmFreeMappingAddress](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreemappingaddress)">MmFreeMappingAddress</a></strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x104</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>所有者の識別タグ</p></td>
<td align="left"><p>呼び出し元が、MDL を所有しないマッピング アドレス空間にマップしようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x105</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元が無効なマッピングのアドレス空間に、MDL をマップしようとしています。 呼び出し元が、無効なアドレスを指定して最も可能性の高い。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x107</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>空でないマッピングのアドレス</p></td>
<td align="left"><p>マッピングの最後のアドレス</p></td>
<td align="left"><p>呼び出し元が、MDL を適切に予約されていないマッピング アドレス空間にマップしようとしています。 呼び出し元を呼び出す必要がある<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapreservedmapping" data-raw-source="[MmUnmapReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapreservedmapping)">MmUnmapReservedMapping</a></strong>呼び出す前に <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpageswithreservedmapping" data-raw-source="[MmMapLockedPagesWithReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpageswithreservedmapping)">MmMapLockedPagesWithReservedMapping</a></strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x108</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>所有者の識別タグ</p></td>
<td align="left"><p>呼び出し元が所有していないマッピングがロックされているアドレス空間をマップ解除しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x109</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元は、明らかに空ではロックされている仮想アドレス領域の割り当てを解除しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10A</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>ロックされているマッピングのアドレス空間内のマッピングの数</p></td>
<td align="left"><p>マップ解除するマッピングの数</p></td>
<td align="left"><p>呼び出し元がロックされているマッピングのアドレス空間に実在するよりも多くのマッピングを解除しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10B</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>マップ解除するマッピングの数</p></td>
<td align="left"><p>呼び出し元が現在マップされていないロックされている仮想アドレス空間の一部をマップ解除しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10C</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>マップ解除するマッピングの数</p></td>
<td align="left"><p>呼び出し元は、ロックされているマッピングのアドレス空間の全体を解除はされません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元がマッピングが含まれていないマッピングのアドレス空間を予約しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x201</p>
<p>0x202</p></td>
<td align="left"><p>最初のマッピング アドレスを予約するには</p></td>
<td align="left"><p>既に予約されているマッピングのアドレス</p></td>
<td align="left"><p>予約へのマッピングの数</p></td>
<td align="left"><p>呼び出し元が予約しようとするマッピングのいずれかが既に予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x300</p></td>
<td align="left"><p>最初のマッピング アドレスを解放するには</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元がマッピングを含まないマッピング アドレス領域を解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x301</p></td>
<td align="left"><p>マッピングのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元が解放することはできませんのマッピングを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x302</p></td>
<td align="left"><p>呼び出し元がリリースしようとするアドレスです。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元が現在マップされていないシステムのアドレスを解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x303</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>リリースへのマッピングの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元が予約されていないマッピング アドレス範囲を解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x304</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>リリースへのマッピングの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元が別の割り当ての途中で始まるマッピング アドレス範囲を解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>呼び出し元がリリースしようとするマッピングの数</p></td>
<td align="left"><p>解放する必要があるマッピングの数</p></td>
<td align="left"><p>呼び出し元がマッピングの数が正しくありませんを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>最初のアドレスのマッピング</p></td>
<td align="left"><p>無料のマッピングのアドレス</p></td>
<td align="left"><p>リリースへのマッピングの数</p></td>
<td align="left"><p>既に呼び出し元がリリースしようとするマッピングの 1 つは、無料です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p>I/O 空間のマッピングのベース アドレス</p></td>
<td align="left"><p>解放するページの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元が、システムが認識される I/O 空間マッピングを解放しようとしています。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

エラーは、パラメーター 1 の値によって示されます。

スタック トレースでは、エラーが発生したドライバーを識別します。

 

 




