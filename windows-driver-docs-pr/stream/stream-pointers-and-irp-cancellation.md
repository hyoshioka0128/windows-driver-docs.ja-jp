---
title: ストリーム ポインターと IRP のキャンセル
description: ストリーム ポインターと IRP のキャンセル
ms.assetid: ce392496-ca07-497d-af8a-709239a7bd5e
keywords:
- ストリーム ポインター WDK AVStream、IRP の取り消し
- IRP 欠航 WDK AVStream
- Irp WDK AVStream のキャンセル
- ロックされているストリーム ポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 784f1ea2f73f89062a22cf82586b00854d8e7d72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377794"
---
# <a name="stream-pointers-and-irp-cancellation"></a>ストリーム ポインターと IRP のキャンセル





フレームにはロックされているストリーム ポインターを参照している場合は、このフレームに対応する IRP をキャンセルできません。 参照してください[ロックと Stream のポインターをロック解除](locking-and-unlocking-stream-pointers.md)します。

次の表では、ミニドライバーは IRP のキャンセルをサポートするために使用できる手法が一覧表示します。 キャンセルの戦略は、左端の列」の説明に従ってのミニドライバーのストリーム アクセスの要件に基づく必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>場合必要があります.</th>
<th>方法</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>単一のアクセス ポイントにデータをストリーミングする簡単なアクセス</p></td>
<td><p>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer" data-raw-source="[&lt;strong&gt;KsPinGetLeadingEdgeStreamPointer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)"> <strong>KsPinGetLeadingEdgeStreamPointer</strong> </a>で、<em>状態</em>パラメーター KSSTREAM_POINTER_STATE_LOCKED に設定します。 呼び出して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)"> <strong>KsStreamPointerUnlock</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerAdvanceOffsetsAndUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)"> <strong>KsStreamPointerAdvanceOffsetsAndUnlock</strong> </a>の処理直後後完了します。</p></td>
<td><p>ポインターの取得とロックの解除の間、スレッドをブロックしない限り、キャンセルに高速の応答性を提供します。</p></td>
</tr>
<tr class="even">
<td><p>無制限のアクセス時間の長さの取り消しのコールバック コンテキストにクレームを放棄することができますが、</p></td>
<td><p>呼び出す<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)"> <strong>KsStreamPointerClone</strong> </a>はロックされているストリーム ポインターを (通常のリーディング エッジ) を複製するには、ロックを解除、および対応を<em>CancelCallback</em>します。 キューのスピン ロックを保持、したがって DISPATCH_LEVEL にし、コールバックが発生します。 したがって、ベンダーから提供された<em>CancelCallback</em>ルーチンは、ミュー テックスを取得するキューの操作や呼び出し関数を実行できません。 代わりに、コールバック ルーチンで、ミニドライバーことを検証、関連付けられているデータ、後ではアクセスされませんを呼び出して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)"> <strong>KsStreamPointerDelete</strong></a>します。</p></td>
<td><p>実装するには困難になりますが、多くの場合、効率的にアクセスし、キャンセルに迅速な応答の最適なバランスを提供します。</p></td>
</tr>
<tr class="odd">
<td><p>定期的なフレームへのアクセスし、アクセスのフレームの消失を許容できます。</p></td>
<td><p>複製のロックを解除し、呼び出しを維持<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock)"> <strong>KsStreamPointerLock</strong> </a>をアクセス時にロックします。 フレームが取り消された、ストリーム ポインターをロックする次の試行が失敗した場合、および、ミニドライバーは呼び出すことができる場合<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)"> <strong>KsStreamPointerDelete</strong></a>します。</p></td>
<td><p>最初のオプションでは、キャンセルに応答性はストリーム ポインターをどのくらいの時間の関数がロックされています。</p></td>
</tr>
<tr class="even">
<td><p>無期限のアクセス時刻およびコールバックへの応答で要求を解放することはできません</p></td>
<td><p>キャンセルを防ぐために時間の任意の長さの複製がロックされているストリーム ポインターを維持します。 複製のストリーム ポインターを作成するには<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)"> <strong>KsStreamPointerClone</strong></a>します。 呼び出して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerlock)"> <strong>KsStreamPointerLock</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerunlock)"> <strong>KsStreamPointerUnlock</strong> </a>をロックまたはクローンのロックを解除します。</p></td>
<td><p>キャンセルに応答性が低下する可能性があります。 使用を検討して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerscheduletimeout" data-raw-source="[&lt;strong&gt;stream pointer timeouts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerscheduletimeout)"><strong>ストリーム ポインター タイムアウト</strong></a>この手法でします。</p></td>
</tr>
</tbody>
</table>

 

フレームにそれを参照するストリーム ポインターがある場合、ミニドライバーを呼び出すことができます[ **KsStreamPointerGetIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointergetirp)このフレームに対応する IRP にアクセスします。 フレームに関連付けられているメモリの記述子リスト (MDL) を取得する[ **KsStreamPointerGetMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointergetmdl)します。

 

 




