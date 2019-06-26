---
title: C28144
description: 、終了時に、キャンセル ルーチン内で C28144 警告 Irp-CancelIrql の IRQL の現在の IRQL 必要があります。
ms.assetid: f89a2f9b-6e84-4696-80c3-79b8760c9b4a
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28144
ms.openlocfilehash: e14aad810dd78a23cd49b80f571c09661c2f59d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364127"
---
# <a name="c28144"></a>C28144


C28144 を警告します。終了時に、Irp の IRQL の時点でのキャンセル ルーチン内&gt;CancelIrql が現在の IRQL をする必要があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>値は、特定の関数では復元されません必要がありますが、終了する前に復元する必要があります。 PREfast は、必要な値に復元されたことを確認できませんでした。</p></td>
</tr>
</tbody>
</table>

 

ときに、ドライバーの[**キャンセル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)ルーチンが終了するの値、 **Irp -&gt;CancelIrql**メンバーは、現在の IRQL ではありません。 ドライバーが呼び出していないときは通常、このエラーが発生します[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))への呼び出しで最も最近提供された IRQL で[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))します。

詳細については*キャンセル*ルーチンを参照してください[キャンセル Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/canceling-irps)します。 この警告に固有の情報を参照してください。 [Irp の検討時にキャンセルを指す](https://docs.microsoft.com/windows-hardware/drivers/kernel/points-to-consider-when-canceling-irps)します。

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

次のコード例では、この警告を引き起こします。

```
IoReleaseCancelSpinLock(PASSIVE_LEVEL);
```

次のコード例は、この警告を回避できます。

```
IoReleaseCancelSpinLock(Irp->CancelIrql);
```

 

 





