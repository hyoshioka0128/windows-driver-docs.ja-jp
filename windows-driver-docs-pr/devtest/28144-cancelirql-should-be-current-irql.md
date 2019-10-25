---
title: C28144
description: キャンセルルーチン内での警告 C28144 は、終了時に、Irp-CancelIrql の IRQL が現在の IRQL である必要があります。
ms.assetid: f89a2f9b-6e84-4696-80c3-79b8760c9b4a
keywords:
- ドライバーの WDK PREfast の一覧に警告が表示される
- ドライバーの WDK PREfast の一覧にエラーが表示される
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28144
ms.openlocfilehash: 434868c580adb4b4f9de52d9698b24f9338bf1a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839594"
---
# <a name="c28144"></a>C28144


警告 C28144: キャンセルルーチン内で、終了時に、Irp&gt;CancelIrql の IRQL が現在の IRQL である必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>値は特定の関数によって復元される必要はありませんが、終了する前に復元する必要があります。 PREfast は、必要な値に復元されたことを確認できませんでした。</p></td>
</tr>
</tbody>
</table>

 

ドライバーの[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンが終了すると、 **Irp&gt;CancelIrql**メンバーの値が現在の IRQL ではなくなります。 通常、このエラーは、ドライバーが[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))の最新の呼び出しで指定された IRQL で[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))を呼び出さない場合に発生します。

*キャンセル*ルーチンの詳細については、「 [irp の取り消し](https://docs.microsoft.com/windows-hardware/drivers/kernel/canceling-irps)」を参照してください。 この警告に固有の情報については、「 [irp をキャンセルする場合の考慮事項](https://docs.microsoft.com/windows-hardware/drivers/kernel/points-to-consider-when-canceling-irps)」を参照してください。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

この警告を elicits するコード例を次に示します。

```
IoReleaseCancelSpinLock(PASSIVE_LEVEL);
```

次のコード例では、この警告を回避します。

```
IoReleaseCancelSpinLock(Irp->CancelIrql);
```

 

 





