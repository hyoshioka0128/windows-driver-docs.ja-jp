---
title: ストリーム ポインターと IRP のキャンセル
description: ストリーム ポインターと IRP のキャンセル
ms.assetid: ce392496-ca07-497d-af8a-709239a7bd5e
keywords:
- ストリームポインター WDK AVStream、IRP キャンセル
- IRP キャンセル WDK AVStream
- Irp WDK AVStream をキャンセルしています
- ロックされたストリームポインター WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5225d26830a089d2e51366d87a361132c58267b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837677"
---
# <a name="stream-pointers-and-irp-cancellation"></a>ストリーム ポインターと IRP のキャンセル





フレームにロックされているストリームポインターがある場合、そのフレームに対応する IRP はキャンセルできません。 「[ストリームポインターのロックとロック解除」を](locking-and-unlocking-stream-pointers.md)参照してください。

次の表は、ミニドライバーが IRP のキャンセルをサポートするために使用できる手法を示しています。 キャンセル戦略は、一番左の列で説明されているように、ミニドライバーのストリームアクセス要件に基づいている必要があります。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>必要に応じて</th>
<th>操作</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>単一のアクセスポイントでのストリームデータへの簡単なアクセス</p></td>
<td><p><em>State</em>パラメーターを KSSTREAM_POINTER_STATE_LOCKED に設定して<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer" data-raw-source="[&lt;strong&gt;KsPinGetLeadingEdgeStreamPointer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-kspingetleadingedgestreampointer)"><strong>KsPinGetLeadingEdgeStreamPointer</strong></a>を呼び出します。 次に、処理が完了した直後に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)"><strong>Ksstreamポインタ unlock</strong></a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerAdvanceOffsetsAndUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointeradvanceoffsetsandunlock)"><strong>KsStreamPointerAdvanceOffsetsAndUnlock</strong></a>を呼び出します。</p></td>
<td><p>は、ポインターの取得とロック解除の間にスレッドがブロックしない限り、キャンセルに迅速な応答性を提供します。</p></td>
</tr>
<tr class="even">
<td><p>アクセス時間の長さは不定ですが、キャンセルコールバックのコンテキストで要求を放棄できます。</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)"><strong>Ksstreampointer clone</strong></a>を呼び出して、ロックされたストリームポインター (通常は先頭のエッジ) を複製し、ロックを解除して、 <em>cancelcallback</em>に応答します。 このコールバックは、キューのスピンロックが保持されている状態で発生します。そのため、DISPATCH_LEVEL になります。 したがって、ベンダーから提供された<em>Cancelcallback</em>ルーチンは、キューの操作を実行したり、ミューテックスを取得する関数を呼び出したりすることはできません。 代わりに、コールバックルーチンでは、ミニドライバーは、関連付けられたデータに後でアクセスできないことを確認してから、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)"><strong>Ksstreamポインター delete</strong></a>を呼び出します。</p></td>
<td><p>を実装するのはより困難ですが、多くの場合、効率的なアクセスとキャンセルへの迅速な対応とのバランスを取ることができます。</p></td>
</tr>
<tr class="odd">
<td><p>フレームへの定期的なアクセスにより、アクセス間のフレームの消失が許容されます。</p></td>
<td><p>ロック解除された複製を保持し、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)"><strong>Ksk Streampoインタ</strong></a>ロックを呼び出してアクセス時にロックします。 フレームがキャンセルされると、次にストリームポインターをロックしようとして失敗し、ミニドライバーは<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete" data-raw-source="[&lt;strong&gt;KsStreamPointerDelete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)"><strong>Ksstreampointer delete</strong></a>を呼び出すことができます。</p></td>
<td><p>最初のオプションと同様に、キャンセルに対する応答性は、ストリームポインターがロックされている期間の関数です。</p></td>
</tr>
<tr class="even">
<td><p>アクセス時間の長さが不定で、コールバックへの応答として要求を放棄できません</p></td>
<td><p>ロックされた複製ストリームポインターを任意の期間保持して、キャンセルされないようにします。 複製ストリームポインターを作成するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone" data-raw-source="[&lt;strong&gt;KsStreamPointerClone&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerclone)"><strong>Ksk streampointer clone</strong></a>を呼び出します。 次に、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock" data-raw-source="[&lt;strong&gt;KsStreamPointerLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerlock)"><strong>Ksstreampointerlock</strong></a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock" data-raw-source="[&lt;strong&gt;KsStreamPointerUnlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock)"><strong>ksstreamポインター unlock</strong></a>を呼び出して、複製をロックまたはロック解除します。</p></td>
<td><p>取り消しに対する応答性が低下する可能性があります。 この手法では、<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout" data-raw-source="[&lt;strong&gt;stream pointer timeouts&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerscheduletimeout)"><strong>ストリームポインタータイムアウト</strong></a>の使用を検討してください。</p></td>
</tr>
</tbody>
</table>

 

フレームにストリームポインターがある場合、ミニドライバーは、このフレームに対応する IRP にアクセスするために、 [**Ksstreampointer Getirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetirp)を呼び出すことができます。 フレームに関連付けられているメモリ記述子リスト (MDL) を取得するには、 [**Ksk Streamポインター Getmdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointergetmdl)を呼び出します。

 

 




