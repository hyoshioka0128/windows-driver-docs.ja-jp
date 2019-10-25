---
title: バグチェック 0xDA SYSTEM_PTE_MISUSE
description: SYSTEM_PTE_MISUSE のバグチェックの値は、0x000000DA です。 これは、不適切な方法でページテーブルエントリ (PTE) ルーチンが使用されていることを示します。
ms.assetid: a9a9f3e9-39b7-4e4a-a326-2f510e0aaa99
keywords:
- バグチェック 0xDA SYSTEM_PTE_MISUSE
- SYSTEM_PTE_MISUSE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_PTE_MISUSE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 023727b030c7644f39bac5bf7173fcfe324a9a7f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827364"
---
# <a name="bug-check-0xda-system_pte_misuse"></a>バグチェック 0xDA: システム\_の PTE\_誤用


システム\_の PTE\_誤用のバグチェックには、0x000000DA の値があります。 これは、不適切な方法でページテーブルエントリ (PTE) ルーチンが使用されていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="system_pte_misuse-parameters"></a>システム\_の PTE\_誤用パラメーター


パラメーター1は違反の種類を示します。 他のパラメーターの意味は、パラメーター1の値によって異なります。

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
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>内部ロック追跡構造のアドレス。</p></td>
<td align="left"><p>メモリ記述子リストのアドレス</p></td>
<td align="left"><p>重複する内部ロック追跡構造のアドレス。</p></td>
<td align="left"><p>解放されているマッピングは重複しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>内部ロック追跡構造のアドレス。</p></td>
<td align="left"><p>システムが解放する必要があるマッピングの数</p></td>
<td align="left"><p>ドライバーが解放を要求しているマッピングの数</p></td>
<td align="left"><p>解放されているマッピングの数が正しくありません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x03</p></td>
<td align="left"><p>検出された最初の内部追跡構造のアドレス。</p></td>
<td align="left"><p>システムが解放を期待するマッピングアドレス</p></td>
<td align="left"><p>ドライバーが解放を要求しているマッピングアドレス</p></td>
<td align="left"><p>解放されているマッピングアドレスが正しくありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x04</p></td>
<td align="left"><p>内部ロック追跡構造のアドレス。</p></td>
<td align="left"><p>システムが必要とするページフレーム番号は、まず MDL 内にある必要があります。</p></td>
<td align="left"><p>MDL の現在の最初のページフレーム番号</p></td>
<td align="left"><p>マップされた MDL の最初のページが、MDL のマップ後に変更されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x05</p></td>
<td align="left"><p>検出された最初の内部追跡構造のアドレス。</p></td>
<td align="left"><p>システムが解放する必要がある仮想アドレス</p></td>
<td align="left"><p>ドライバーが解放を要求している仮想アドレス</p></td>
<td align="left"><p>解放されている MDL の開始仮想アドレスが、MDL のマップ後に変更されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x06</p></td>
<td align="left"><p>ドライバーによって指定された MDL</p></td>
<td align="left"><p>ドライバーによって指定された仮想アドレス</p></td>
<td align="left"><p>解放するマッピングの数 (ドライバーによって指定)</p></td>
<td align="left"><p>解放されている MDL は、マップされていない (または現在は) ことができませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>初期マッピング</p></td>
<td align="left"><p>マッピングの数</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>(Windows 2000 のみ)マッピング範囲が二重に割り当てられています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08</p></td>
<td align="left"><p>初期マッピング</p></td>
<td align="left"><p>呼び出し元が解放しているマッピングの数</p></td>
<td align="left"><p>システムが解放する必要があるマッピングの数</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元は、正しくない数のマッピングを解放するように要求しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x09</p></td>
<td align="left"><p>初期マッピング</p></td>
<td align="left"><p>呼び出し元が解放しているマッピングの数</p></td>
<td align="left"><p>システムによって判断されたマッピングインデックスは既に無料です</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元は複数のマッピングを解放するように要求していますが、そのうち少なくとも1つは割り当てられていません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0A</p></td>
<td align="left"><p><strong>1:</strong>ドライバーは、MDL で "バグチェックが失敗しました" を要求しました。</p>
<p><strong>0:</strong>ドライバーは、MDL に "バグチェックの失敗" を要求しませんでした。</p></td>
<td align="left"><p>呼び出し元が割り当てているマッピングの数</p></td>
<td align="left"><p>要求されたマッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が0のマッピングを割り当てようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0B</p></td>
<td align="left"><p>破損したマッピング</p></td>
<td align="left"><p>呼び出し元が割り当てているマッピングの数</p></td>
<td align="left"><p>要求されたマッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)この割り当ての時点で、マッピング一覧は既に破損しています。 破損したマッピングは、可能な限り低いマッピングアドレスの下にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0C</p></td>
<td align="left"><p>破損したマッピング</p></td>
<td align="left"><p>呼び出し元が割り当てているマッピングの数</p></td>
<td align="left"><p>要求されたマッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)この割り当ての時点で、マッピング一覧は既に破損しています。 破損したマッピングは、可能な限り低いマッピングアドレスの上にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0D</p></td>
<td align="left"><p>初期マッピング</p></td>
<td align="left"><p>呼び出し元が解放しているマッピングの数</p></td>
<td align="left"><p>マッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が0のマッピングを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0E</p></td>
<td align="left"><p>初期マッピング</p></td>
<td align="left"><p>呼び出し元が解放しているマッピングの数</p></td>
<td align="left"><p>マッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元がマッピングを解放しようとしていますが、ガードマッピングが上書きされています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0F</p></td>
<td align="left"><p>存在しないマッピング</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングの数</p></td>
<td align="left"><p>解放されるマッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が、存在しないマッピングを解放しようとしています。 存在しないマッピングは、可能な限り低いマッピングアドレスの下にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10</p></td>
<td align="left"><p>存在しないマッピング</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングの数</p></td>
<td align="left"><p>解放されるマッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が、存在しないマッピングを解放しようとしています。 存在しないマッピングは、可能な限り高いマッピングアドレスの上にあります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x11</p></td>
<td align="left"><p>存在しないマッピング</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングの数</p></td>
<td align="left"><p>解放されるマッピングプールの種類</p></td>
<td align="left"><p>(Windows 2000 のみ)呼び出し元が、存在しないマッピングを解放しようとしています。 存在しないマッピングは、マッピングアドレス空間のベースにあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x100</p></td>
<td align="left"><p>要求されているマッピングの数</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>このルーチンの呼び出し元を呼び出したルーチンのアドレス。</p></td>
<td align="left"><p> 呼び出し元が0のマッピングを要求しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x101</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>所有者の識別タグ</p></td>
<td align="left"><p> 呼び出し元が、所有していないマッピングアドレス範囲を解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x102</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングアドレス空間は、明らかに空です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x103</p></td>
<td align="left"><p>無効なマッピングのアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>マッピングアドレス空間内のマッピングの数</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングアドレス空間は、まだ予約されています。 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping" data-raw-source="[MmUnmapReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping)">MmUnmapReservedMapping</a></strong></p>
<p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreemappingaddress" data-raw-source="[MmFreeMappingAddress](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreemappingaddress)">MmFreeMappingAddress</a></strong>の前に呼び出す必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x104</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>所有者の識別タグ</p></td>
<td align="left"><p>呼び出し元は、それ自身が所有していないマッピングアドレス空間に MDL をマップしようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x105</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元が、無効なマッピングアドレス空間に MDL をマップしようとしています。 呼び出し元は、ほとんどの場合、無効なアドレスを指定しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x107</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>空でないマッピングのアドレス</p></td>
<td align="left"><p>最後のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元が、適切に予約されていないマッピングアドレス空間に MDL をマップしようとしています。 呼び出し元は、 <strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpageswithreservedmapping" data-raw-source="[MmMapLockedPagesWithReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpageswithreservedmapping)">MmMapLockedPagesWithReservedMapping</a></strong>を呼び出す前に<strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping" data-raw-source="[MmUnmapReservedMapping](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapreservedmapping)">MmUnmapReservedMapping</a></strong>を呼び出す必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x108</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>所有者の識別タグ</p></td>
<td align="left"><p>呼び出し元は、所有していないロックされたマッピングアドレス空間のマップを解除しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x109</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元は、明らかに空のロックされた仮想アドレス空間のマップを解除しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10A</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>ロックされたマッピングアドレス空間内のマッピングの数</p></td>
<td align="left"><p>マップを解除するマッピングの数</p></td>
<td align="left"><p>呼び出し元は、ロックされたマッピングアドレス空間に実際に存在するよりも多くのマッピングをマップ解除しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10B</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>マップを解除するマッピングの数</p></td>
<td align="left"><p>呼び出し元が、現在マップされていないロックされた仮想アドレス空間の一部をマップ解除しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10C</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元の識別タグ</p></td>
<td align="left"><p>マップを解除するマッピングの数</p></td>
<td align="left"><p>呼び出し元は、ロックされたマッピングアドレス空間全体のマップを解除していません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元は、マッピングを含まないマッピングアドレス空間を予約しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x201</p>
<p>0x202</p></td>
<td align="left"><p>予約する最初のマッピングアドレス</p></td>
<td align="left"><p>既に予約されているマッピングのアドレス</p></td>
<td align="left"><p>予約するマッピングの数</p></td>
<td align="left"><p>呼び出し元が予約しようとしているマッピングのいずれかが既に予約されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x300</p></td>
<td align="left"><p>解放する最初のマッピングアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元は、マッピングが含まれていないマッピングアドレス空間を解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x301</p></td>
<td align="left"><p>マッピングのアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元は、解放が許可されていないマッピングを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x302</p></td>
<td align="left"><p>呼び出し元が解放しようとしているアドレス。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>呼び出し元が、現在マップされていないシステムアドレスを解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x303</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>解放するマッピングの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元は、予約されていないマッピングアドレス範囲を解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x304</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>解放するマッピングの数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元が、異なる割り当ての途中で始まるマッピングアドレス範囲を解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x305</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングの数</p></td>
<td align="left"><p>解放する必要があるマッピングの数</p></td>
<td align="left"><p>呼び出し元は、間違った数のマッピングを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x306</p></td>
<td align="left"><p>最初のマッピングアドレス</p></td>
<td align="left"><p>フリーマッピングアドレス</p></td>
<td align="left"><p>解放するマッピングの数</p></td>
<td align="left"><p>呼び出し元が解放しようとしているマッピングの1つは、既に無料です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p>I/o スペースマッピングのベースアドレス</p></td>
<td align="left"><p>解放するページ数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>呼び出し元は、システムが認識していない i/o 空間マッピングを解放しようとしています。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

このエラーは、パラメーター1の値によって示されます。

スタックトレースによって、エラーの原因となったドライバーが特定されます。

 

 




