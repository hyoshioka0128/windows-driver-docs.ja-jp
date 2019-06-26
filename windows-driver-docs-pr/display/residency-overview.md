---
title: 常駐の概要
description: 常駐の概要
ms.assetid: E610C2B8-354C-4DF5-8B25-6472A9313B15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a0d9f717edf193d8acec81ae3f6111c070d4a4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385657"
---
# <a name="residency-overview"></a>常駐の概要


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


現在の割り当てと修正プログラムの場所一覧と共に情報すべてコマンド バッファーを作成、ユーザー モード ドライバーを作成します。 この情報は、2 つの目的のビデオ メモリ マネージャーによって使用されます。

-   実際のセグメントのアドレスを持つコマンド バッファーのパッチを適用して、グラフィックス処理ユニット (GPU) エンジンに送信する前に、割り当ての一覧と修正プログラムの場所のリストが使用されます。 Windows Display Driver Model (WDDM) v2 での GPU 仮想アドレスのサポートは、この修正プログラムの必要性を削除します。
-   割り当ての一覧と修正プログラムの場所のリストは、割り当てのコントロールの保存場所、ビデオ メモリ マネージャーによって使用されます。 ビデオ メモリ マネージャーにより、特定のエンジンの実行をコマンド バッファーが送信される前にコマンド バッファーによって参照されるすべての割り当てが常駐行われています。

新しい保存場所のモデルの導入に伴い、コマンドごとのバッファーの一覧ではなく、デバイス上の保存場所を明示的なリストに移動中です。 ビデオ メモリ マネージャーがそのデバイスに属する任意のコンテキストが実行をスケジュールする前に特定のデバイスの保存場所の要件の一覧ですべての割り当てが常駐していることを確認します。

保存場所を管理するために、ユーザー モード ドライバー アクセスすることが 2 つ新しいデバイス ドライバー インターフェイス (Ddi) [ *MakeResident* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)と[*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)新しい実装するために必要になるほか、 [ *TrimResidency* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_trimresidencyset)コールバック。 *MakeResident*デバイスの保存場所の要件の一覧に 1 つまたは複数の割り当てを追加します。 *削除*そのリストから複数割り当てのいずれかが削除されます。 *TrimResidency*ユーザー モード ドライバーが常駐要件を削減する必要があるときにそのコールバックがビデオ メモリ マネージャーによって呼び出されます。

[*MakeResident* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)と[*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)つまり複数の呼び出しに内部参照カウントを保持する更新された*MakeResident*等しい数が必要になります*削除*の呼び出しを実際には、割り当てを削除します。

モデルでは、新しい保存場所、コマンドごとのバッファーの割り当てと修正プログラムの場所のリストが緩やかに変化段階的です。これらのリストに存在するには一部のシナリオで、これらの保存場所を制御がされなくなります。

**重要な**  WDDM v2 での保存場所は、デバイスの保存場所要件の一覧が排他的制御されます。 これは、すべてのエンジンのすべての API と GPU の間で当てはまります。

 

## <a name="span-idphasingoutallocationandpatchlocationlistspanspan-idphasingoutallocationandpatchlocationlistspanspan-idphasingoutallocationandpatchlocationlistspanphasing-out-allocation-and-patch-location-list"></a><span id="Phasing_out_allocation_and_patch_location_list"></span><span id="phasing_out_allocation_and_patch_location_list"></span><span id="PHASING_OUT_ALLOCATION_AND_PATCH_LOCATION_LIST"></span>割り当てと修正プログラムの場所のリストを徐々 に


割り当てと修正プログラムの場所の一覧のロールでは、新しい保存場所のモデルの導入により大幅に削減は取得し、ハードウェア支援によるスケジュールの導入に伴いは完全に破棄に移動実際にします。

モデルでは、パケットに基づいてスケジュール、割り当ての一覧は次のように存在し続けます。

-   エンジンの GPU の仮想アドレス指定をサポートしていない場合、割り当ての一覧と修正プログラムの場所のリストは引き続き存在、ただし、修正プログラムの適用のためだけに使用して、保存場所を制御する必要がなくなります。 ユーザー モード ドライバーと各種の通常 Ddi でカーネル モード ドライバーの両方に提供される、割り当ての一覧と修正プログラムの場所のリストが常駐ではない割り当てへの参照と、GPU スケジューラの送信を拒否し、デバイスを(失わ) エラーが発生します。 この操作モードでは従来と見なされ、将来のリリースのハードウェアをアドレス指定が仮想 GPU のサポートを受けるすべての GPU エンジンを予定します。 この操作モードが失われます将来のバージョン、WDDM のことが必要です。
-   仮想 GPU をサポートしているエンジンのアドレス指定、新しいコンテキストの作成フラグ (**DXGK\_contextinfo です\_いいえ\_修正\_REQUIRED**) があることを示す追加特定コンテキストでは、すべての修正プログラムを必要としません。 このフラグを指定すると、修正プログラムの場所のリストは割り当てられません、割り当てが非常に小さく一覧 (16 個のエントリ) のみが割り当てられます。 割り当ての一覧は、書き込み参照プライマリ サーフェスにし、目的のための追跡に使用されます。 GPU のスケジューラは、プライマリの画面に発生する可能性のあるフリップに関しては、そのバッファーの実行を正しく同期することがあるようにプライマリの画面にで特定のコマンド バッファーが書き込み中に把握する必要があります。

同様に、割り当ての一覧は、カーネル モード ドライバーで使用*存在*パスを今すぐ、ソースと宛先の詳細については、ドライバーに情報を渡す、*存在*操作。 割り当てリストは引き続きに関するパラメーターを渡す存在このコンテキストでただし、割り当て一覧はしないするための保存場所。 修正プログラムの適用を必要とする Gpu 上、*存在*割り当ての一覧が今日のパッチの適用前情報が表示されます、*存在*場合は、リソースのいずれかのスケジュール設定する前にパケットを再修正プログラムが適用されますGPU 上で、スケジューラにキューに時間と実行のスケジュールされている時間の間のメモリ内で移動します。

次の表では、WDDM ドライバーを v2 は、さまざまなユーザー モード ドライバーやカーネル モード ドライバー Ddi で、割り当てと修正プログラムの場所のリストを受信することが予想されるときにまとめたものです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GPU エンジン</th>
<th align="left">割り当てのリストかどうか</th>
<th align="left">修正プログラムの場所のリストですか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">GPU 仮想アドレスはサポートされません (修正プログラムの適用を必要と、既定の)</td>
<td align="left"><p>はい、フル サイズが、純粋な目的で修正プログラムの適用に使用します。</p>
送信 (失わ) エラーと、送信された、スケジューラによって拒否されている入力デバイスが常駐割り当てへの参照が発生します。</td>
<td align="left">[はい]、完全なサイズ。</td>
</tr>
<tr class="even">
<td align="left">GPU 仮想アドレスのサポート (<strong>DXGK_CONTEXTINFO_NO_PATCHING_REQUIRED</strong>フラグを設定)</td>
<td align="left"><p>はい、16 個のエントリ。</p>
コマンド バッファーが書き込んでいるため、存在する場合は、プライマリのサーフェスを参照します。 Lip 表示コント ローラー上で発生すると、GPU スケジューラによって同期に使用します。 デバイスの保存場所の要件の一覧で、プライマリ画面必要があります。 または参照は拒否されます。</td>
<td align="left">X</td>
</tr>
<tr class="odd">
<td align="left">GPU 仮想アドレスのサポート + ハードウェアのスケジュール設定</td>
<td align="left">X</td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

 

 





