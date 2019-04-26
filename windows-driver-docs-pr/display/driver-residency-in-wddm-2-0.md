---
title: WDDM 2.0 でのドライバー常駐
description: ここでは、Windows Display Driver Model (WDDM) 2.0 用に保存場所の変更をドライバーの詳細に説明します。 説明されている機能では、Windows 10 以降で使用できます。
ms.assetid: 9BD0138A-E957-4675-8E08-2750825A5C87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86f179b00a5a0300b8354ccebaa25bc4013fbe5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358442"
---
# <a name="driver-residency-in-wddm-20"></a>WDDM 2.0 でのドライバー常駐


ここでは、Windows Display Driver Model (WDDM) 2.0 用に保存場所の変更をドライバーの詳細に説明します。 説明されている機能では、Windows 10 以降で使用できます。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


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
<td align="left"><p><a href="residency-overview.md" data-raw-source="[Residency overview](residency-overview.md)">保存場所の概要</a></p></td>
<td align="left"><p>新しい保存場所のモデルの導入に伴い、コマンドごとのバッファーの一覧ではなく、デバイス上の保存場所を明示的なリストに移動中です。 ビデオ メモリ マネージャーがそのデバイスに属する任意のコンテキストが実行をスケジュールする前に特定のデバイスの保存場所の要件の一覧ですべての割り当てが常駐していることを確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="allocation-usage-tracking.md" data-raw-source="[Allocation usage tracking](allocation-usage-tracking.md)">割り当ての使用状況の追跡</a></p></td>
<td align="left"><p>消滅の割り当てリスト、ビデオ メモリ マネージャーはなくなりました可視性を特定のコマンド バッファーで参照されている割り当て。 このため、ビデオ メモリ マネージャーが割り当ての使用状況を追跡し、関連の同期を処理するために、位置。 この責任はユーザー モード ドライバーに今すぐ分類されます。 具体的には、ユーザー モード ドライバーは、割り当てと名前の変更に直接アクセスする CPU に対して同期を処理する必要があります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="offer-and-reclaim-changes.md" data-raw-source="[Offer and reclaim changes](offer-and-reclaim-changes.md)">提供し、変更を再利用</a></p></td>
<td align="left"><p>WDDM v2、関連する要件の<em>提供</em>と<em>回収</em>緩和されています。 ユーザー モード ドライバーをプランを使用し、内部の割り当てを解放する必要なくなりました。 使用してアプリケーションのアイドル状態や中断されたドライバーの内部リソースの削除は、<strong>トリミング</strong>Microsoft DirectX 11.1 で導入された API です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="access-to-non-resident-allocation.md" data-raw-source="[Access to non-resident allocation](access-to-non-resident-allocation.md)">非常駐割り当てへのアクセス</a></p></td>
<td align="left"><p>グラフィックス プロセッシング ユニット (GPU) への常駐ではない割り当ては無効であり、エラーを生成したアプリケーションの削除、デバイスになります。</p>
<p>これには、エラーが発生したエンジンがかどうかを示す仮想 GPU をサポートするかどうかに依存するこのような無効なアクセスの処理の 2 つの異なるモデルがあります。</p>
<ul>
<li>アクセスが無効ですが、ユーザー モード ドライバーに存在することはない割り当てを参照する割り当てリストを送信するときに発生エンジンの GPU の仮想アドレス指定をサポートし、割り当てとメモリ参照の修正プログラムに修正プログラムの場所のリストを使用しない場合、デバイス (つまり、ユーザー モード ドライバーと呼ばれる<a href="https://msdn.microsoft.com/library/windows/hardware/dn906357" data-raw-source="[&lt;em&gt;MakeResidentCb&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn906357)"> <em>MakeResidentCb</em> </a>その割り当てに)。 これが発生したグラフィックスのカーネルに欠陥のあるコンテキストまたはデバイスがエラーで保存されます。</li>
<li>エンジンの GPU 仮想アドレス指定をサポートせず、無効な GPU 仮想アドレスにアクセスする場合か、仮想アドレスの割り当てはありませんが、有効な割り当てはまたは常駐が作成されていないため、GPU は、発生が予想される、割り込みの形式で復旧不可能なページ フォールトします。 ページ フォールトの割り込みが発生したときに、カーネル モード ドライバーは新しいページ フォールト通知によるグラフィックス カーネルにエラーを転送する必要があります。 この通知を受信するとは、グラフィックス カーネルはリセット エラーが発生したエンジンのエンジンを開始し、欠陥のあるコンテキスト/デバイスをエラーにします。 エンジンのリセットが成功しなかった場合、グラフィックス カーネルは、フル アダプター全体のタイムアウト検出と復旧 (TDR) をすると、エラーを昇格します。</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="process-residency-budgets.md" data-raw-source="[Process residency budgets](process-residency-budgets.md)">プロセスの保存場所の予算</a></p></td>
<td align="left"><p>WDDM v2 では、メモリの量を維持できる常駐の予算のプロセスが割り当てられます。 この予算では、時間の経過と共に変更できますが、通常はのみが適用されるとき、システムがメモリ不足。 Microsoft direct3d12 では、前に、予算がの形式では、ユーザー モード ドライバーによって処理される<em>トリミング</em>通知と<em>MakeResident</em>によるエラー <strong>STATUS_NO_MEMORY</strong>します。 <em>TrimToBudget</em>通知、 <a href="https://msdn.microsoft.com/library/windows/hardware/dn906355" data-raw-source="[&lt;em&gt;Evict&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn906355)"><em>削除</em></a>、および失敗した<a href="https://msdn.microsoft.com/library/windows/hardware/dn906357" data-raw-source="[&lt;em&gt;MakeResident&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/dn906357)"> <em>MakeResident</em> </a>で最新の予算を返すすべての呼び出し、整数のフォーム<strong>NumBytesToTrim</strong>新しい予算に適合するためにトリミングする必要がある量を示す値です。</p></td>
</tr>
</tbody>
</table>

 

 

 





