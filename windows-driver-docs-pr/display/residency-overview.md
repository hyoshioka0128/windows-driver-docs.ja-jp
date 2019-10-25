---
title: 常駐の概要
description: 常駐の概要
ms.assetid: E610C2B8-354C-4DF5-8B25-6472A9313B15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cecf4e6edd8aa39cc68904b2598ca62bd6977a15
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829575"
---
# <a name="residency-overview"></a>常駐の概要


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


現在、ユーザーモードドライバーは、ビルドするすべてのコマンドバッファーと共に割り当てとパッチの場所の一覧の情報を作成します。 この情報は、次の2つの目的でビデオメモリマネージャーによって使用されます。

-   割り当てリストとパッチの場所の一覧は、実際のセグメントアドレスを使用してコマンドバッファーにパッチを適用してから、GPU (グラフィックスプロセッシングユニット) エンジンに送信するために使用されます。 Windows Display Driver Model (WDDM) v2 での GPU 仮想アドレスのサポートにより、この修正プログラムの適用は不要になります。
-   割り当ての一覧と修正プログラムの場所の一覧は、割り当ての保存を制御するためにビデオメモリマネージャーによって使用されます。 ビデオメモリマネージャーを使用すると、コマンドバッファーによって参照される割り当ては、特定のエンジンの実行にコマンドバッファーが送信される前に常駐するようになります。

新しいレジデンシーモデルが導入されたことで、常駐サービスは、コマンドごとのバッファー一覧ではなく、デバイス上の明示的なリストに移行されます。 ビデオメモリマネージャーでは、そのデバイスに属するすべてのコンテキストの実行がスケジュールされる前に、特定のデバイスの常駐要件リストに対するすべての割り当てが確実に存在することを確認します。

レジデンシーサービスを管理するために、ユーザーモードドライバーは2つの新しいデバイスドライバーインターフェイス (DDIs)、 [*Makeresident*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb) 、および[*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)にアクセスできます。また、新しい[*TrimResidency*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_trimresidencyset)コールバックを実装するために必要です。 *Makeresident*は、デバイスの保存要件リストに1つまたは複数の割り当てを追加します。 削除すると、その一覧から1つ以上の割り当てが*削除され*ます。 *TrimResidency*コールバックは、その常駐要件を減らすためにユーザーモードドライバーが必要な場合に、ビデオメモリマネージャーによって呼び出されます。

また、 [*makeresident*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_makeresidentcb)と[*削除*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_evictcb)も内部参照カウントを保持するように更新されています。つまり、 *makeresident*を複数回呼び出す場合は、割り当てを実際に削除するために同数の*削除*呼び出しが必要になります。

新しいインサイトでは、コマンドごとのバッファー割り当てと修正プログラムの場所の一覧が徐々に徐々に減少しています。これらのリストはいくつかのシナリオに存在しますが、これらの一覧は、常駐サービスを制御できなくなります。

  WDDM v2 の**重要な**は、デバイスの保存要件の一覧によってのみ制御されます。 これは、GPU のすべてのエンジンとすべての API で当てはまります。

 

## <a name="span-idphasing_out_allocation_and_patch_location_listspanspan-idphasing_out_allocation_and_patch_location_listspanspan-idphasing_out_allocation_and_patch_location_listspanphasing-out-allocation-and-patch-location-list"></a><span id="Phasing_out_allocation_and_patch_location_list"></span><span id="phasing_out_allocation_and_patch_location_list"></span><span id="PHASING_OUT_ALLOCATION_AND_PATCH_LOCATION_LIST"></span>段階的に割り当てとパッチの場所の一覧を表示する


割り当てとパッチの場所の一覧の役割は、新しい常駐モデルの導入によって大幅に削減され、実際にはハードウェアによるスケジュール設定の導入によって完全に解消されます。

パケットベースのスケジュールモデルでは、割り当て一覧は次のようになります。

-   GPU 仮想アドレス指定をサポートしていないエンジンでは、割り当て一覧と修正プログラムの場所の一覧は引き続き存在しますが、修正プログラムの適用目的でのみ使用され、常駐を制御することはできなくなります。 割り当て一覧と修正プログラムの場所の一覧は、通常のさまざまな DDIs のユーザーモードドライバーとカーネルモードドライバーの両方に提供されますが、常駐していない割り当てを参照すると、GPU スケジューラによって送信が拒否され、デバイスが挿入されます。エラー (失われた)。 この操作モードは従来と見なされ、すべての GPU エンジンが将来のハードウェアリリースで GPU 仮想アドレスのサポートを受けることを想定しています。 このモードの操作は、WDDM の将来のバージョンでは削除される予定です。
-   GPU 仮想アドレス指定をサポートするエンジンの場合、新しいコンテキスト作成フラグ (**DXGK\_CONTEXTINFO\_\_パッチの\_適用を必要としません**) が追加され、特定のコンテキストで修正プログラムを適用する必要がないことが示されます。 このフラグが指定されている場合、修正プログラムの場所の一覧は割り当てられず、非常に小さな割り当てリスト (16 個のエントリ) のみが割り当てられます。 割り当て一覧は、プライマリサーフェイスへの書き込み参照を追跡し、その他の目的には使用されません。 GPU スケジューラは、特定のコマンドバッファーがプライマリサーフェイスに書き込んでいることを認識する必要があります。これにより、プライマリサーフェイスで発生する可能性のあるフリップに関して、そのバッファーの実行を適切に同期することができます。

同様に *、現在の操作の*ソースと宛先に関する情報をドライバーに渡すために、現在のカーネルモードドライバー*のパスで*割り当てリストが使用されます。 このコンテキストでは、割り当てリストは引き続きパラメーターを渡すために存在しますが、割り当てリストは常駐環境では使用されません。 パッチの適用を必要とする Gpu では、現在*の割り当てリストには、現在*の動作と同様にパッチ前の情報が含まれています。また、リソースが次の期間の間にメモリ内で移動された場合は、スケジュールされる前に、*現在*のパケットに再適用されます。スケジューラのキューに登録され、GPU での実行がスケジュールされている時刻。

次の表は、WDDM v2 ドライバーがさまざまなユーザーモードドライバーおよびカーネルモードドライバー DDIs で割り当てと修正プログラムの場所の一覧を受け取る必要がある場合の概要を示しています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">GPU エンジン</th>
<th align="left">割り当て一覧</th>
<th align="left">パッチの場所の一覧</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">GPU 仮想アドレスがサポートなし (修正プログラムの適用、既定値)</td>
<td align="left"><p>はい。完全なサイズですが、更新プログラムの適用のためにのみ使用します。</p>
存在しない割り当てへの参照によって、送信デバイスがエラーになり (失われ)、スケジューラによって送信が拒否されます。</td>
<td align="left">はい、完全なサイズです。</td>
</tr>
<tr class="even">
<td align="left">GPU 仮想アドレスサポート (<strong>DXGK_CONTEXTINFO_NO_PATCHING_REQUIRED</strong>フラグセット)</td>
<td align="left"><p>はい、16エントリ。</p>
コマンドバッファーによって書き込まれたプライマリサーフェイス (存在する場合) を参照します。 GPU スケジューラが、ディスプレイコントローラーでの lip の同期に使用します。 プライマリサーフェイスは、デバイスの保存要件の一覧に既に存在している必要があります。存在しない場合、参照は拒否されます。</td>
<td align="left">必須ではない</td>
</tr>
<tr class="odd">
<td align="left">GPU 仮想アドレスサポート + ハードウェアスケジュール</td>
<td align="left">必須ではない</td>
<td align="left">必須ではない</td>
</tr>
</tbody>
</table>

 

 

 





