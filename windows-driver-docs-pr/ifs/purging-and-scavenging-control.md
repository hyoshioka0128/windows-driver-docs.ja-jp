---
title: 削除と清掃の制御
description: 削除と清掃の制御
ms.assetid: 103b05e6-333a-441a-a4f8-784ae43df59e
keywords:
- RDBSS WDK ファイルシステム、消去と清掃の構造
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、消去と清掃の構造
- WDK ネットワークリダイレクターの削除
- WDK ネットワークリダイレクターの清掃
- FOBX 構造体
- FOBX 構造のクリーンアップ WDK ネットワークリダイレクター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbbec1f501ee3c9f7504611df665b8468037747c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841015"
---
# <a name="purging-and-scavenging-control"></a>削除と清掃の制御


## <span id="ddk_purging_and_scavenging_control_if"></span><span id="DDK_PURGING_AND_SCAVENGING_CONTROL_IF"></span>


RDBSS には、不要になったときに FOBX 構造を消去して清掃するための多くのルーチンが用意されています。

クリーンアップ時には、ファイルオブジェクトに関連付けられたユーザーハンドルはこれ以上ありません。 このような場合、終了とクリーンアップの間の時間枠は、Memory Manager と Cache Manager によって管理される追加の参照によって決まります。 RDBSS は、別のスレッドで実行されるスカベンジャープロセスを使用して、不要な FOBX およびその他の構造を清掃し、削除します。

現時点では、SRV\_呼び出し、NET\_ROOT および V\_NET\_ルート構造に清掃が実装されています。 FCB 清掃は個別に処理されます。 FOBX は、常に同期的に完了する必要があります。 清掃を終了するために有効にする必要があるデータ構造は、SRV\_オープン構造のみです。

現在、RDBSS に実装されているスカベンジャープロセスでは、ファイナライズの清掃が必要になるまで、システムリソースは消費されません。 清掃を終了するようにマークされる最初のエントリは、そのスカベンジャーに対してタイマー要求がポストされます。 現在の実装では、タイマー要求はワンショットタイマー要求としてポストされます。 これは、エントリが完了するまでの時間間隔に関して保証がないことを意味します。 スカベンジャーアクティブ化メカニズムは、後の段階での微調整の候補となる可能性があります。

RDBSS の削除と清掃のルーチンには、次のものが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs" data-raw-source="[&lt;strong&gt;RxPurgeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxpurgeallfobxs)"><strong>RxPurgeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、ネットワークミニリダイレクターに関連付けられているすべての FOBX 構造を削除します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs" data-raw-source="[&lt;strong&gt;RxPurgeRelatedFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxpurgerelatedfobxs)"><strong>RxPurgeRelatedFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、NET_ROOT 構造体に関連付けられているすべての FOBX 構造体を削除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs" data-raw-source="[&lt;strong&gt;RxScavengeAllFobxs&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxscavengeallfobxs)"><strong>RxScavengeAllFobxs</strong></a></p></td>
<td align="left"><p>このルーチンは、特定のネットワークミニリダイレクターデバイスオブジェクトに関連付けられているすべての FOBX 構造を清掃します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot" data-raw-source="[&lt;strong&gt;RxScavengeFobxsForNetRoot&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scavengr/nf-scavengr-rxscavengefobxsfornetroot)"><strong>RxScavengeFobxsForNetRoot</strong></a></p></td>
<td align="left"><p>このルーチンは、特定の NET_ROOT 構造体に関連付けられているすべての FOBX 構造体を清掃します。</p></td>
</tr>
</tbody>
</table>

 

 

 




