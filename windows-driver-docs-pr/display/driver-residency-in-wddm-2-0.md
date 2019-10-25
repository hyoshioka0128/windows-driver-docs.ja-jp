---
title: WDDM 2.0 でのドライバー常駐
description: このセクションでは、Windows Display Driver Model (WDDM) 2.0 のドライバーの常駐に関する変更について詳しく説明します。 ここで説明する機能は、Windows 10 以降で使用できます。
ms.assetid: 9BD0138A-E957-4675-8E08-2750825A5C87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3803719ea4fe3ba9b1418f175d4e73246c4096c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838985"
---
# <a name="driver-residency-in-wddm-20"></a>WDDM 2.0 でのドライバー常駐


このセクションでは、Windows Display Driver Model (WDDM) 2.0 のドライバーの常駐に関する変更について詳しく説明します。 ここで説明する機能は、Windows 10 以降で使用できます。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="residency-overview.md" data-raw-source="[Residency overview](residency-overview.md)">常駐の概要</a></p></td>
<td align="left"><p>新しいレジデンシーモデルが導入されたことで、常駐サービスは、コマンドごとのバッファー一覧ではなく、デバイス上の明示的なリストに移行されます。 ビデオメモリマネージャーでは、そのデバイスに属するすべてのコンテキストの実行がスケジュールされる前に、特定のデバイスの常駐要件リストに対するすべての割り当てが確実に存在することを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="allocation-usage-tracking.md" data-raw-source="[Allocation usage tracking](allocation-usage-tracking.md)">割り当ての使用状況の追跡</a></p></td>
<td align="left"><p>割り当て一覧が表示されなくなると、ビデオメモリマネージャーは特定のコマンドバッファーで参照されている割り当てを認識できなくなります。 このため、ビデオメモリマネージャーは、割り当ての使用状況を追跡し、関連する同期を処理するための位置ではなくなりました。 この責任は、ユーザーモードドライバーに分類されるようになります。 特に、ユーザーモードドライバーは、割り当てへの直接の CPU アクセスと名前の変更に関して、同期を処理する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="offer-and-reclaim-changes.md" data-raw-source="[Offer and reclaim changes](offer-and-reclaim-changes.md)">変更の提供と再利用</a></p></td>
<td align="left"><p>WDDM v2 では、<em>オファー</em>と<em>回収</em>に関する要件が緩和されています。 ユーザーモードドライバーは、内部割り当てでプランを使用して再利用するために必要なくなりました。 アイドル/中断されたアプリケーションは、Microsoft DirectX 11.1 で導入された<strong>Trim</strong>API を使用して、ドライバーの内部リソースを排除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="access-to-non-resident-allocation.md" data-raw-source="[Access to non-resident allocation](access-to-non-resident-allocation.md)">非常駐割り当てへのアクセス</a></p></td>
<td align="left"><p>グラフィックス処理ユニット (GPU) が常駐していない割り当てへのアクセスは無効なため、エラーを生成したアプリケーションに対してデバイスが削除されます。</p>
<p>障害が発生したエンジンが GPU 仮想アドレス指定をサポートしているかどうかによって、このような無効なアクセスを処理する2つの異なるモデルがあります。</p>
<ul>
<li>GPU 仮想アドレス指定をサポートしておらず、割り当てとパッチの場所の一覧を使用してメモリ参照を修正するエンジンの場合、無効なアクセスが発生するのは、ユーザーモードドライバーが割り当て一覧を送信するときに、デバイス (つまり、ユーザーモードドライバーはその割り当てで<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb" data-raw-source="[&lt;em&gt;MakeResidentCb&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)"><em>MakeResidentCb</em></a>を呼び出していません)。 このようにすると、グラフィックスカーネルによって、問題のあるコンテキストまたはデバイスのエラーが発生します。</li>
<li>GPU 仮想アドレスをサポートしていても、無効な GPU 仮想アドレスにアクセスするエンジンについては、仮想アドレスの背後に割り当てられていないか、有効な割り当てがあり、まだ常駐していないため、GPU は割り込みの形式での回復不可能なページフォールト。 ページフォールト割り込みが発生した場合、カーネルモードドライバーは、新しいページフォールト通知を使用してグラフィックスカーネルにエラーを転送する必要があります。 この通知を受信すると、グラフィックスカーネルによって、障害が発生したエンジンでエンジンのリセットが開始され、エラーが発生したコンテキストまたはデバイスのエラーが発生します。 エンジンのリセットが失敗した場合、グラフィックスカーネルは、完全なアダプター全体のタイムアウト検出と復旧 (TDR) にエラーを昇格させます。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="process-residency-budgets.md" data-raw-source="[Process residency budgets](process-residency-budgets.md)">プロセス常駐の予算</a></p></td>
<td align="left"><p>WDDM v2 では、プロセスには、常駐可能なメモリの量に関する予算が割り当てられます。 この予算は時間の経過と共に変化しますが、一般に、システムのメモリが不足している場合にのみ適用されます。 Microsoft Direct3D 12 より前の場合、この予算は、ユーザーモードドライバーによって、 <em>Trim</em>通知と<strong>STATUS_NO_MEMORY</strong>での<em>makeresident</em>エラーの形式で処理されます。 <em>TrimToBudget</em> Notification、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb" data-raw-source="[&lt;em&gt;Evict&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)"><em>削除</em></a>、および失敗した<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb" data-raw-source="[&lt;em&gt;MakeResident&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)"><em>makeresident</em></a>のすべての呼び出しは、新しい予算に適合するためにどのくらいの量を切り捨てる必要があるかを示す整数<strong>numbytestotrim</strong>値の形式で、最新の予算を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 





