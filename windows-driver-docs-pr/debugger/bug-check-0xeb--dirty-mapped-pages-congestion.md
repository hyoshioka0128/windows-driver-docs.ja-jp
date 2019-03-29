---
title: バグ チェック 0xEB DIRTY_MAPPED_PAGES_CONGESTION
description: DIRTY_MAPPED_PAGES_CONGESTION のバグ チェックでは、0x000000EB の値を持ちます。 これは、空きページが継続的に使用しないことを示します。
ms.assetid: 7a73dc74-fe40-4c0c-9c33-b0af3709bf43
keywords:
- バグ チェック 0xEB DIRTY_MAPPED_PAGES_CONGESTION
- DIRTY_MAPPED_PAGES_CONGESTION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DIRTY_MAPPED_PAGES_CONGESTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e5194d7d4db78510c64181acbbf04119881c678a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574116"
---
# <a name="bug-check-0xeb-dirtymappedpagescongestion"></a>バグ チェック 0xEB:ダーティ\_マップ済み\_ページ\_輻輳


DIRTY\_マップ済み\_ページ\_輻輳のバグ チェックが 0x000000EB の値を持ちます。 これは、空きページが継続的に使用しないことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="dirtymappedpagescongestion-parameters"></a>ダーティ\_マップ済み\_ページ\_輻輳パラメーター


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
<td align="left"><p>1</p></td>
<td align="left"><p>ダーティ ページの合計数</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>ページファイル宛てのダーティ ページの数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>Windows Server 2003 ののみ:ページ単位でのバグ チェック時に使用可能な非ページ プールのサイズ</p>
<p>Windows Vista およびそれ以降のバージョン:予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>Windows Server 2003 ののみ:取り残されたは現在移行のページの数</p>
<p>Windows Vista およびそれ以降のバージョン:最新の変更の書き込みエラーの状態</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ファイル システム ドライバー スタックはデッドロックし、ファイル システム宛てのほとんどの変更されたページ。 ファイル システムは操作不可であるために、データを失うことがなく変更済みページの再利用できるため、システムがクラッシュします。 エラーのスタック内のファイル システムまたはフィルター ドライバーがあります。

全般的なメモリの統計情報を表示するには、使用、 [ **! vm 3** ](-vm.md)拡張機能。

このバグ チェックの次の理由により発生します。

-   デッドロック、変更、または割り当てられたページ ライターでは、ドライバーがブロックされています。 この例には、ミュー テックスのデッドロックやファイル システム ドライバーまたはフィルター ドライバーのメモリをページアウトへのアクセスが含まれます。 これは、ドライバーのバグを示します。

    パラメーター 1 または 2 のパラメーターが大きい場合は、可能性です。 使用[ **! vm 3**](-vm.md)します。

-   記憶装置ドライバーが要求を処理していません。 この例は、孤立したキューと応答していないドライブです。 これは、ドライバーのバグを示します。

    パラメーター 1 または 2 のパラメーターが大きい場合は、可能性です。 使用[ **! 0 7 処理**](-process.md)します。

-   Windows Server 2003 ののみ:十分なプールは、記憶域スタックが変更されたページを書き込むに使用できます。 これは、ドライバーのバグを示します。

    パラメーター 3 が小さい場合は、これは、可能性があります。 使用[ **! vm** ](-vm.md)と[ **! poolused 2**](-poolused.md)します。

 

 




